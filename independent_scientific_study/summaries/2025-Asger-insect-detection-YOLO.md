# A General Method for Detection and Segmentation of Terrestrial Arthropods in Images
- **Authors:** Asger Svenning, Guillaume Mougeot, Jamie Alison, Daphne Chevalier, Nisa Chavez Molina, Song-Quan Ong, Kim Bjerge,
Juli Carrillo, Toke Thomas Høye, and Quentin Geissmann
- **Year:** 2025
- **PDF:** [2025-Asger-insect-detection-YOLO](../papers/2025-Asger-insect-detection-YOLO.pdf)

---

## . Problem or Motivation
- Current insect detection models have modest performance and poor generalization across varying scales, appearances, and densities. 
- FlatBug aims to provide a universal insect/arthropod detector that worksout-of-the-box on diverse imaging conditions without retraining.

## 2. Methodology
- Combines a YOLOv8-based instance segmentation model with a novel pyramid tiling inference strategy for size-agnostic detection. Trained on a highly diverse dataset of 6,131 images with ~113,550 annotated insects spanning 23 different lab and field image sources. 
- Uses stratified leave-one-out and leave-two-out cross-validation to rigorously evaluate generalization (testing how performance drops when certain sub-datasets are excluded from training).

## 3. Datasets and Experiments
- The FlatBug dataset integrates many smaller datasets (including citizen science images, field trap images, lab photos, etc.) to cover a broad taxonomic range.
- Experiments measured detection and segmentation performance (F1 score) on both validation sets and completely held-out sub-datasets to assess generalizability.

## 4. Results and Findings
- FlatBug achieved an average F1 ≈ 94% on the validation set.
- Importantly, when tested on entirely new environments (datasets omitted from training), performance dropped only ~7.1% (relative) in F1, demonstrating strong generalization without retraining.
-  The tiling approach allows inference on arbitrarily large images and effective detection of both very small and very large insects in the same image. 
- Code and trained models are released openly for use and further evaluation.

## 5. Relevance to Insect Detection
- Directly targets insect/arthropod detection and segmentation, showing that a single model can handle multiple species and image domains with minimal performance loss.
- This is highly relevant for ecological monitoring, where one may deploy one model on varied inputs (lab scans, field photos, trap images) instead of training new models for each scenario.

## 6. Limitations and Future Work
- FlatBug’s approach, while promising, hasn’t been peer-reviewed yet. 
- The model is segmentation-based and fairly large (uses YOLOv8 under the hood), which might be challenging for real-time edge deployment. Future work might involve distilling FlatBug into lighter models or extending it to video data and additional arthropod groups (e.g., incorporating flying insect tracking).

## 7. Evaluation
- **Priority:** High. (It establishes a new benchmark for general-purpose insect detectors.)
- **Use for Thesis:** Yes. (Crucial if discussing state-of-the-art insect detection or building a baseline general model in this domain.)
