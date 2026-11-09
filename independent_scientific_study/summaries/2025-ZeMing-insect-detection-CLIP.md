# CLIBD: BRIDGING VISION AND GENOMICS FOR BIODIVERSITY MONITORING AT SCALE
- **Authors:** ZeMing Gong, Austin T. Wang, Xiaoliang Huo, Joakim Bruslund Haurum, Scott C. Lowe, Graham W. Taylor, Angel X. Chang
- **Year:** 2025
- **PDF:** [2025-ZeMing-insect-detection-CLIP.pdf](../papers/2025-ZeMing-insect-detection-CLIP.pdf)

---

## 1. Problem or Motivation
- Traditional approaches classify insect images or DNA barcodes separately, but many species lack labeled images while DNA sequence (barcodes) are available.
- The motivation is to leverage both modalities to improve species identification, especially for zero-shot recognition of novel species.

## 2. Methodology
- Introduces CLIBD, a multimodal model using a CLIP-like contrastive learning framework.
- Images, DNA barcode sequences, and textual taxonomic labels are embedded into a shared feature space where matching image–DNA–label triplets align closely.
- By training on known species with both images and DNA, the model learns a joint representation enabling it to classify species from image or DNA inputs (or both) even without explicit training on that particular species (zero-shot).

## 3. Datasets and Experiments
- Trained and evaluated on the BIOSCAN insect datasets (e.g., BIOSCAN-1M, BIOSCAN-5M) which contain over a million insect images each paired with a COI DNA barcode and species label.
- Tasks include zero-shot image classification (identify species from images whose labels were not seen during training) and multimodal retrieval (match images with DNA sequences).

## 4. Results and Findings
- The multimodal CLIBD model significantly outperforms single-modality baselines. It improved classification accuracy by over 8% on zero-shot species recognition compared to image-only or DNA-only models.
- In practical terms, the model can accurately classify previously unseen insect species from images by leveraging the DNA embedding and textual label space, demonstrating a powerful biodiversity monitoring tool.

## 5. Relevance to Insect Detection
- Though focusing on classification rather than object detection, this work is highly relevant for insect species identification.
- It suggests that incorporating biological data (DNA) and language (species names/descriptions) can greatly enhance the recognition of insect species, even those without extensive image datasets.
- For insect detection systems, such a model could be used downstream to identify detected insects to species level, or to discover new species in imagery via DNA similarity.

## 6. Limitations and Future Work
- The requirement of DNA barcodes means this approach is limited to scenarios where specimens can be collected and sequenced or when working with datasets like BIOSCAN.
- It’s also a large model trained on millions of data points, so deploying it in real-time detection pipelines may be challenging.
- Future work could explore few-shot learning of new species, or integrating ecological metadata (location, time) to further improve accuracy.

## 7. Evaluation
- **Priority:** Medium  (Innovative multimodal approach but more relevant to classification and taxonomy than to real-time detection.) 
- **Use for Thesis:** Maybe (Include if the thesis touches on species-level identification or multimodal AI for biodiversity; otherwise, it can be peripheral to core detection methods.)
