# Datasets

## What is in this repository

```
datasets/real/
  images/                 92 annotated pitfall-trap photographs (~602 MB)
  labels/labels.json      the annotations (Label Studio export, 25 MB)
  real_split_groups.csv   the group-disjoint split: 19 tray groups -> train/valid/test
  READ_ME.txt             the dataset's own note
datasets/inputs/
  selected_classes_original_20000.csv   177,718 rows - the balanced BIOSCAN selection
  cutouts_metadata.csv                  177,718 rows - route, dish radius, band, area ratio
  quality.csv                           177,718 rows - the quality tags alone
  cutout_blocklist.csv                  25 rows - specimens the generator must exclude
datasets/synthetic/
  {train,valid,test}_annotations.coco.json   the full mixed-corpus record
  mix_boxes.csv, mix_summary.csv             per-box geometry and the split summary
  3dtrab_coco_TESTSPLIT.json                 the 14 held-out real frames alone
```

The real photographs are here because **they cannot be regenerated**. Everything else in the pipeline
is a function of these photographs, the BIOSCAN cutouts, and the notebooks.

The split is by **tray group**, not by frame — frames of one tray are near-duplicates
(the same tray at three focal heights), so splitting by frame would leak. It works out
as train 46 frames / 1,890 insects, valid 31 / 733, test 14 / 479, over 19 groups.
`SPLIT_FRACS` in `mix_real_and_synthetic.ipynb` is 60/20/20 **of real insects**, not of
frames, which is why the frame counts are not a clean 60/20/20 of 91.

Two things to know before using the validation split: it is 31 frames but only **six
groups**, and `3D08` alone contributes 26 of them. And the test set is 14 frames from
six groups, which is why a tray-level bootstrap of the real results gives 95 %
intervals 0.17–0.33 wide.

## The synthetic corpus: annotations here, images on Ares

`datasets/synthetic/` carries the full COCO record for the 27,873-image mixed
corpus (1,115,392 annotations across the three splits). The **tray images** are
**72 GB** and live on Ares storage at

    students/ma_atul_dind/data/MA_Atul_Ares/insect_dataset_coco_20000_mix/

Everything that can be checked without pixels — class balance, box geometry, the
split, the real/synthetic mix — is answerable from the annotations alone.

## What is NOT here, and why

| dataset | server path | approx. size |
|---|---|---|
| synthetic trays | `insect_dataset_coco_20000_mix` | **72 GB** (27,000 trays, measured) |
| synthetic + real mix | `insect_dataset_mixed` | similar |
| tiled corpus | `insect_dataset_mixed_tiled1536` | 166,850 tiles (not measured) |
| flat-bug YOLO views | `sept_run/flatbug_yolo_mixed`, `..._tiled1536` | conversions of the above |
| BIOSCAN cutouts | `DATASET_20000_mix/cutouts` | 177,718 RGBA PNGs (not measured) |

The tray corpus is **72 GB**, measured. The other two were never measured — get the
real numbers before deciding anything about them:

```bash
cd /data/MA_Atul_Ares
du -sh insect_dataset_coco_20000_mix insect_dataset_mixed \
       insect_dataset_mixed_tiled1536 DATASET_20000_mix/cutouts \
       sept_run/flatbug_yolo_mixed sept_run/flatbug_yolo_tiled1536
```

72 GB for the trays alone, before the tiles and cutouts, and git is the wrong
container for it. Repository storage quota is not the only limit that bites: LFS storage is usually
quota'd separately and far more tightly, every clone pays for it, and GitLab caps
individual file sizes independently of the quota.

## Is the synthetic corpus reproducible from the notebooks?

**Mostly, but not bit-for-bit — so do not treat regeneration as a substitute for
archiving it.** The generator sets `RANDOM_SEED = 42` and seeds both `random` and
`numpy`, and `mix_real_and_synthetic.ipynb` uses `SEED = 0`. But:

- at least one generator RNG is created unseeded with no fallback
  (`_trng = np.random.default_rng()`), and several helpers fall back to an unseeded
  generator if no `rng` is passed;
- segmentation runs BiRefNet on a GPU, which is not deterministic in general.

So a re-run produces a *statistically equivalent* corpus, not the same files. The
reported numbers were measured on the corpus that exists on the server.

## Recommended: archive the corpus, don't commit it

Put the rendered corpora and the cutouts in a **separate archive** — Zenodo (you are
already minting a DOI for the generator), the university's research data store, or
simply the server with a documented path — and commit only a manifest here:

```bash
cd /data/MA_Atul_Ares
for d in insect_dataset_coco_20000_mix insect_dataset_mixed_tiled1536; do
  find "$d" -type f | wc -l
  du -sh "$d"
  md5sum "$d"/*/_annotations.coco.json      # the annotation files are the thing to pin
done
```

A manifest of counts, sizes and annotation-file checksums is a few kilobytes, makes
the archive verifiable, and gives the thesis something citable. That is what an
examiner or a later reader actually needs; a 72 GB clone is not.

## Checks you can run on what is here

Applying the generator's own filter to `datasets/inputs/cutouts_metadata.csv` —
`area_ratio` within [0.30, 4.0], with missing values kept, exactly as `_keep()` does —
yields **148,285** cutouts, the figure the thesis reports. The blocklist's 25 rows are
the 21 out-of-class specimens plus 4 fragment photographs the generator warns about.

In `datasets/synthetic/`, the train split holds 17,028 images of which 828 are real:
46 distinct photographs x `REAL_OVERSAMPLE = 18`. Valid and test carry their 31 and 14
frames once each. That is the whole real/synthetic mix, checkable without any pixels.
