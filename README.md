# Deep Learning based Insect Detection for Biodiversity Monitoring

Code and trained models for the MSc thesis of the Atul Santhosh
(Philipps-Universität Marburg, Distributed Systems Group, 2026).

The work compares **RF-DETR-Large** and **flat-bug (YOLOv8-L)** trained on a synthetic
corpus of composed pitfall-trap tray images and real trap photographs and evaluated using test set.

This repository holds the **notebooks** and the **trained weights**. The thesis
document, the cached predictions and the analysis scripts live elsewhere.

```
notebooks/          the pipeline, end to end, from BIOSCAN download onward
datasets/real/      the 92 annotated photographs, labels, group-disjoint split
datasets/inputs/    pre-computed inputs (selection CSV, cutout metadata, blocklist)
datasets/synthetic/ COCO annotations for the full 27,873-image mixed corpus
models/             the five trained models + their training configs
```

> ### ⚠️ The synthetic tray **images** are not in this repository
>
> The corpus is **72 GB** approx after generation.
>
> What **is** here is the complete annotation record for that corpus
> (`datasets/synthetic/`) — every image entry, every box, every class, for all
> three splits. That is enough to audit class balance, box statistics and the
> split without a single pixel. Only pixel-level work needs the Ares copy.

Everything needed to run the pipeline is here. Nothing further to fetch.

## The pipeline, in the order it runs

| # | notebook | what it does |
|---|---|---|
| 0 | `bioscan_5m.ipynb` | downloads BIOSCAN-5M via `bioscan_dataset`, filters to the target orders, samples the balanced pool and writes `selected_classes_original_20000.csv` + the specimen images |
| 1 | `generate_synthetic_trays_DATASET_server.ipynb` | segments BIOSCAN specimens (BiRefNet) and composes them onto tray backgrounds; produces the 27,000-tray corpus |
| 1b | `inspect_and_prune.ipynb` | audits the BIOSCAN cutout pool and **writes the blocklist**. Run this first — the generator asserts the blocklist exists and refuses to run without it. |
| 2 | `mix_real_and_synthetic.ipynb` | builds the group-disjoint real split and mixes real photographs into the synthetic corpus |
| 3 | `train_flatbug_fullres.ipynb` / `train_flatbug_tiled_fullres.ipynb` | flat-bug (YOLOv8-L), whole-tray and tiled |
| 4 | `train_rfdetr_fullres.ipynb` / `train_rfdetr_tiled_fullres.ipynb` | RF-DETR-Large, whole-tray and tiled |
| 5 | `final_comparison_fullres.ipynb` | scores every model on the synthetic splits and the real photographs |


**Step 1 is not optional.** Skipping it silently puts back 21 specimens whose order is
outside the class list, plus four fragment photographs, and the rare-order recipes give
those far more tray time than their count suggests.


## Configuration, as run

| | flat-bug whole | flat-bug tiled | RF-DETR whole | RF-DETR tiled |
|---|---|---|---|---|
| input / resolution | 1536 | 1536 (= TILE) | 1536 | 1536 |
| epochs (cap) | 100 | 30 | 100 | 30 |
| batch | 4 | 4 | 4 × 4 accum | 4 × 4 accum |
| optimiser | SGD, LR 0.01 | inherits | LR 1e-4, encoder 1.5e-4 | same |
| early stopping | patience 20 | patience 10 | patience 20 | patience 10 |
| EMA | — | — | off | off |
| seed | 42, deterministic | 42, deterministic | **none set** | **none set** |

Tiling: `TILE = 1536`, `OVERLAP = 256`, six tiles per tray. For RF-DETR
`RESOLUTION == TILE`, so tiles are fed 1:1 with no resize. The `@1536` in the model
names is this number.

Three things worth knowing before reading the numbers:

- **The epoch caps are not the training length.** Early stopping selected epoch 34
  (whole-tray) and epoch 25 (tiled).
- **RF-DETR was never seeded.** `TrainConfig.seed` defaults to `None` and the training
  call passes nothing, so its run-to-run variance is not controlled the way flat-bug's
  is. The `random.seed(42)` in the whole-tray notebook only picks which images to plot.
- **The real training share is 46 distinct photographs repeated 18 times**
  (`REAL_OVERSAMPLE = 18` in `mix_real_and_synthetic.ipynb`). That is five percent of
  the training signal, but not five percent of the variety.

## Environment

Two kernels, and they are not interchangeable — the comparison notebook loads one
model family per kernel and silently skips what it cannot import:

- **flat-bug**: Python 3.11, PyTorch, Ultralytics 8.3.124
- **RF-DETR**: Python 3.10, PyTorch, `rf-detr` 1.7.1

Every notebook reads its base directory from `MA_BASE`, defaulting to the compute
server's path:

```bash
export MA_BASE=/path/to/your/data      # then start Jupyter
```

That is the only path you should ever need to set. It resolves `datasets/`,
`models/` and every intermediate the pipeline writes.

## Datasets

`datasets/inputs/` holds the intermediate artefacts so the chain can be re-entered
without repeating the expensive steps:

| file | rows | what it is |
|---|---|---|
| `selected_classes_original_20000.csv` | 177,718 | the balanced BIOSCAN selection (step 0's output) |
| `cutouts_metadata.csv` | 177,718 | one row per segmented cutout: route, dish radius, quality band, area ratio |
| `quality.csv` | 177,718 | the quality tags alone |
| `cutout_blocklist.csv` | 25 | specimens the generator must exclude — it asserts this file exists |

Applying the generator's own filter (`area_ratio` within [0.30, 4.0], missing kept)
to `cutouts_metadata.csv` yields **148,285** cutouts, which is the figure the thesis
reports. The blocklist's 25 rows are the 21 out-of-class specimens plus 4 fragment
photographs.

`datasets/synthetic/` holds the COCO annotations for the whole mixed corpus — the
record of exactly what the models were trained and evaluated on:

| split | images | of which real | annotations |
|---|---|---|---|
| train | 17,028 | 828 | 682,265 |
| valid | 5,431 | 31 | 216,893 |
| test | 5,414 | 14 | 216,234 |
| **total** | **27,873** | **873** | **1,115,392** |

27,000 synthetic trays plus 873 real image entries. The 828 in train is 46 distinct
photographs x `REAL_OVERSAMPLE = 18`; valid and test carry their 31 and 14 frames
once each. Also here: `mix_boxes.csv` (per-box geometry for the whole corpus),
`mix_summary.csv`, and `3dtrab_coco_TESTSPLIT.json` — the 14 held-out real frames
alone, safe to score a model against.

**The images themselves are on Ares**, not here:
`students/ma_atul_dind/data/MA_Atul_Ares/insect_dataset_coco_20000_mix/`

`datasets/real/` holds the **92 annotated pitfall-trap photographs**, their
annotations and the group-disjoint split — the part of the input that cannot be
regenerated from anything else. Via Git LFS; ~630 MB.

The synthetic corpora (rendered trays, tiles, BIOSCAN cutouts) are **not** here — the
tray corpus alone is 72 GB. `datasets/DATASETS.md` gives the paths and the case for
archiving rather than committing — including the fact
that regeneration is *statistically* equivalent but **not bit-for-bit**, because one
generator RNG is unseeded and GPU segmentation is not deterministic.
