# Title: A multi-modal dataset for insect biodiversity with imagery and DNA at the trap and individual level
- **Authors:** Johanna Orsholm, John Quinto, Hannu Autto, Gaia Banelyte, Nicolas Chazot, Jeremy deWaard, Stephanie deWaard, Arielle Farrell, Brendan Furneaux, Bess Hardwick, Nao Ito, Amlan Kar, Oula Kalttopää, Deirdre Kerdraon, Erik Kristensen, Jaclyn McKeown, Tommi Mononen, Ellen Nein, Hanna Rogers, Tomas Roslin, Paula Schmitz, Jayme Sones, Maija Sujala, Amy Thompson, Evgeny V. Zakharov, Iuliia Zarubiieva, Akshita Gupta, Scott C. Lowe, Graham W. Taylor (et al.)
- **Year:** 2025
- **PDF:** [papers/2025-Johanna-insect-segment-indentification-MassID45.pdf](../papers/2025-Johanna-insect-segment-indentification-MassID45.pdf)

---

## 1. Problem or Motivation
Most insect ML datasets are based on *individual specimen* images, but ecological monitoring typically produces **unsorted bulk samples** (e.g., Malaise trap catches) photographed as a single tray image. Bulk images contain **tiny, densely packed and sometimes overlapping insects**, making both counting and taxonomic labeling difficult. The paper introduces **MassID45** to bridge this training-data gap by pairing bulk-tray imagery with **DNA-based taxonomic signal** and expert annotations, enabling research on (i) bulk-sample computer vision, and (ii) multi-modal biodiversity monitoring.

## 2. Methodology
- **Two-level multi-modal data creation:** for each of 45 bulk samples, provide bulk images + metabarcoding, and also sort specimens for individual imaging + DNA barcoding.
- **AI-assisted bulk annotation pipeline:** generate initial masks via **watershed segmentation**, refine and correct in **TORAS** (human-in-the-loop), then label arthropod masks with expert taxonomy.
- **Sample-specific taxonomies:** restrict label search space per bulk image using the set of taxa confirmed from **individual DNA barcodes**, while allowing expert override.
- **Tiny-instance segmentation benchmark setup:** treat bulk images as a **single-class instance segmentation** task (arthropod vs background) and export annotations in **MS-COCO** format.
- **Tiling + SAHI inference:** split high-res bulk images into **512×512** tiles with **60% overlap**, then merge predictions with **SAHI** using non-max merging.

## 3. Datasets and Experiments
- Dataset(s) used:  
  - **MassID45**: 45 bulk arthropod samples (Sweden + Finland, 2021) with **49 bulk images**.
  - Bulk-image annotations: ~**17.9k** arthropod instance masks (plus debris/unknown/edge categories in the annotation workflow).
  - Individual-level data: ~**35.6k** individual specimen images + COI barcode sequences.
- Model(s) or architecture(s):  
  - **Zero-shot / foundation-style baselines:** CutLER; Grounding DINO + SAM 2.1; Florence-2 + SAM 2.1; Gemini 2.0 Flash + SAM 2.1.
  - **Supervised baselines (fine-tuned):** Mask R-CNN, Mask2Former, Mask DINO (Detectron2; ResNet-50 backbone pretrained on MS-COCO).
- Metrics:  
  - MS-COCO-style mask AP: **AP50:5:95**, **AP50**, **AP75**, plus size-specific **APS/APM/APL** (with small/medium/large thresholds adapted from iSAID due to tiny instances).
- Baseline comparisons:  
  - Compare **zero-shot** generalization vs **supervised** fine-tuning on MassID45, using the same tiling + SAHI inference pipeline.

## 4. Results and Findings
- **Zero-shot is substantially weaker than supervised:** best zero-shot method (Grounding DINO + SAM 2.1) reaches **AP50:5:95 ≈ 27.1**, while the best supervised model (Mask DINO) reaches **AP50:5:95 ≈ 43.5**.
- Supervised models produce far fewer false positives/negatives on dense tray patches, but **debris vs tiny insects** remains a major error mode.
- Dataset statistics emphasize the “tiny object” regime: a large majority of masks fall in the **small** category, motivating tiling/SAHI and small-object evaluation.

## 5. Relevance to Insect Detection
- Directly targets your thesis setting: **bulk tray / unsorted sample detection** with dense, tiny instances (more realistic than single-specimen imagery).
- Provides a practical, reproducible **annotation + training pipeline** for tiny instance segmentation (watershed → TORAS → expert labels; then tiling + SAHI).
- The two-level design (bulk + individuals) supports **multi-modal learning** ideas: DNA-derived taxonomic evidence can guide visual models, and images can help estimate **absolute abundance** where metabarcoding struggles.
- Strong benchmark for comparing **foundation/zero-shot** models vs **classical supervised** segmentation in a hard biological domain.

## 6. Limitations and Future Work
- **Annotation completeness drops** in extremely dense samples (hundreds to thousands of individuals); small pale taxa (e.g., springtails) are especially hard to separate from debris.
- **Imaging constraints:** some insects are blurry/low-detail; paper suggests super-resolution as a possible direction.
- **Domain shift risk:** models fine-tuned on their imaging setup may need transfer learning for other tray setups / lighting / cameras.
- **Taxonomy uncertainty + DNA/image mismatch:** metabarcoding and individual barcoding can disagree due to primer bias, contamination, and sequencing failures.

## 7. Evaluation
- **Priority:** High
- **Use for Thesis:** Yes
