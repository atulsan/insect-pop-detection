# Topic Overview – Insect Detection

This document provides an overview of the main themes and representative literature covered in the independent scientific study.

# Rating Overview (criterias) ★★★★★

- Suitability for lab-style insect imagery (like BIOSCAN-1M/5M).
- Fine-grained species classification ability.
- Openness to directly understand lab based images.

---

## 1. Object Detection

**Objective:** Understand general-purpose object detection architectures relevant to insect detection.

**Key Papers:**
- [2025 - RF-DETR vs YOLOv12 Comparison – Introduces RF-DETR and compares it with YOLOv12 on agricultural datasets.](./papers/2025-Ranjan-object-detection-RF-DETR.pdf) - [Summary](./summaries/2025-Ranjan-object-detection-RF-DETR.md) - ★★★☆☆ 
- [2024 – DETRs Beat YOLOs on Real-Time Object Detection – Proposes RT-DETR and demonstrates transformer-based detectors matching or surpassing YOLO in speed and accuracy.](./papers/2024-Yian-object-detection-DETR.pdf) - [Summary](./summaries/2024-Yian-object-detection-DETR.md) - ★★★★☆

**Notes:** 
- CNN-based models (like YOLO) have given way to effective transformers (like DETR variants) in modern object detection. 
- Although DETR models now perform in real-time with greater accuracy on complex scenes, YOLO is still popular for speed.
- Transformers are useful for fine-grained tasks because of their exceptional ability to handle context and occlusion.

---

## 2. Insect Detection

**Objective:** Explore detection approaches tailored to insect morphology and environmental challenges.

**Key Papers:**

- [2025 – Svenning - General Arthropod Detection & Segmentation (FlatBug) – YOLOv8-based model with tiling strategy for universal insect detection and instance segmentation.](./papers/2025-Asger-insect-detection-YOLO.pdf) - [Summary](./summaries/2025-Asger-insect-detection-YOLO.md) - ★★★★★

- [2025 – Orsholm et al. – MassID45 (Multi-modal bulk-tray insect dataset) – Introduces a dataset pairing bulk tray imagery with per-individual instance segmentation masks + taxonomic labels (17k+ specimens), and DNA data at both trap and individual level for biodiversity monitoring.](./papers/2025-Johanna-insect-segment-indentification-MassID45.pdf) - [Summary](./summaries/2025-Johanna-insect-segment-indentification-MassID45.md) - ★★★★★

- [2025 - ZeMing - using CLIP-style contrastive learning to align images,barcode DNA, and text-based representations of taxonomic labels in a unified em-bedding space uses BIOSCAN-1M.](./papers/2025-ZeMing-insect-detection-CLIP.pdf) - [Summary](./summaries/2025-ZeMing-insect-detection-CLIP.md) - ★★★★★
- [2022 – Kundur & Mallikarjuna, Deep Learning for Pest Classification – EfficientNet-B7 + Faster R-CNN for high-precision pest identification.](./papers/2022-Niranjan-insect-detection-CNN.pdf) - [Summary](./summaries/2022-Niranjan-insect-detection-CNN.md) - ★★★☆☆
- [2025 – Deng - AMS-YOLO for Tiny Pests – YOLOv8n enhanced with attention & multi-scale modules for small insect detection.](./papers/2025-Leilei-insect-detection-AMS-YOLO.pdf) - [Summary](./summaries/2025-Leilei-insect-detection-AMS-YOLO.md) - ★★★★☆
- [2025 – Chen - Key-FG DETR for Camouflaged Locusts – Transformer detector with fine-grained queries to spot camouflaged pests.](./papers/2025-Chen-insect-detection-Transformer.pdf) - [Summary](./summaries/2025-Chen-insect-detection-Transformer.md) - ★★★☆☆
- [2024 – Sittinger - Insect Detect DIY Camera Trap – Low-cost edge device (Raspberry Pi + OAK-D camera) for real-time pollinator monitoring.](./papers/2024-Sittinger-insect-detection-Light.pdf) - [Summary](./summaries/2024-Sittinger-insect-detection-Light.md) - ★★★☆☆

**Other Papers:**

- [2023-Huang-insect-detection-SVM+HOG](./papers/2023-Huang-insect-detection-SVM+HOG.pdf) - [Summary](./summaries/2023-Huang-insect-detection-SVM+HOG.md) - ★☆☆☆☆
- [2024-Zheng-insect-detection-YOLO](./papers/2024-Zheng-insect-detection-YOLO.pdf) -[Summary](./summaries/2024-Zheng-insect-detection-YOLO.md) - ★★☆☆☆
- [2024-Venkata-insect-detection-Transformer](./papers/2024-Venkata-insect-detection-Transformer.pdf) - [Summaries](./summaries/2024-Venkata-insect-detection-Transformer.md) - ★★★★★
- [2024-Karim-insect-detection-Transformer](./papers/2024-Karim-insect-detection-Transformer.pdf) - [Summaries](./summaries/2024-Karim-insect-detection-Transformer.md) - ★★★★☆
- [2024-Yang-insect-detection-Light](./papers/2024-Yang-insect-detection-Light.pdf) - [Summaries](./summaries/2024-Yang-insect-detection-Light.md) - ★★☆☆☆
- [2024-Jean-insect-detection-Light](./papers/2024-Jean-insect-detection-Light.pdf) - [Summaries](./summaries/2024-Jean-insect-detection-Light.md) ★★☆☆☆


**Notes:** 
- Small object size, camouflage, and species similarity make it difficult to detect insects. 
- SVM+HOG, two hand-crafted feature methods, perform well on small datasets but poorly in real-world scenarios.
- For real-time pest detection, CNN and YOLO-based models are the most popular, and attention modules improve results.
- Transformers are improving camouflaged insect spotting and fine-grained detection.
- Motion-enhanced video detectors and multimodal learning (DNA + image) are emerging trends.
---

## 3. Datasets for Insects

**Objective:** Summarize available datasets for insect detection and classification.

**Key Datasets:**
- BIOSCAN_5M: Insect Dataset is a landmark collection of approximately 5 million hand-labeled microscope images
- BIOSCAN_1M: Insect Dataset is a landmark collection of approximately 1.1 million hand-labeled microscope images
- AMI Dataset (AMI-GBIF & AMI-Traps): A large-scale benchmark for fine-grained insect identification in the wild, combining ~2.5M curated insect images from GBIF (citizen science + museum collections) with expert-annotated camera trap images for out-of-distribution evaluation.
- MassID45: A multi-modal bulk arthropod dataset with tray imagery + per-individual instance segmentation masks and taxonomic labels (17k+ individuals), paired with DNA data at both trap level (metabarcoding) and individual level (barcodes).

**Primary Reference:** 
- [BIOSCAN-5M Insect Dataset (2025) – ~5.15 million images of ~35,458 arthropod species (98% insects) with DNA barcodes and geo-data](./papers/2025-Zahra-insect-dataset-BIOSCAN_5M.pdf)
- [BIOSCAN-1M Insect Dataset (2023) – ~1.13 million images of ~12,491 insect specimens paired with DNA barcodes (a precursor to BIOSCAN-5M)](./papers/2023-Zahra-insect-dataset-BIOSCAN_1M.pdf)
- [AMI Dataset (2024) – Insect Identification in the Wild: AMI-GBIF (~2.5M images, 5,364 moth species curated from GBIF) and AMI-Traps (2,893 camera-trap images with 52,948 annotated insects across 5 countries), designed for fine-grained and out-of-distribution insect classification](./papers/2024-Adithya-AMI-dataset.pdf)
- [MassID45 (2025) – A multi-modal dataset for insect biodiversity with imagery and DNA at the trap and individual level (bulk tray images + instance segmentation masks + taxonomic labels; paired trap-level and individual-level DNA)](./papers/2025-Johanna-insect-segment-indentification-MassID45.pdf)

**Notes:**
- The largest lab-quality insect image datasets, each associated with a DNA barcode, are BIOSCAN-5M and BIOSCAN-1M which are perfect for our use case. They facilitate the fine-grained classification of tens of thousands of species.
- AMI complements BIOSCAN by explicitly targeting in-the-wild generalization: models are trained on curated GBIF-style images (AMI-GBIF) and evaluated on challenging camera-trap imagery (AMI-Traps).
- These are combined in recent efforts to create reliable insect detection models.
- MassID45 complements BIOSCAN by focusing on *bulk sample / tray* imagery with dense, tiny instances and expert masks—useful for benchmarking tiling/SAHI-style pipelines and estimating abundance alongside DNA-based taxonomy.
---

## 4. Approaches to Insect Detection

| Approach Type                | Method / Architecture                          | Key Innovation                                                                        | Performance                                                     | Application Focus                                                   | Year       | Representative Papers & Links                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------|------------------------------------------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------|---------------------------------------------------------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Traditional Machine Learning** | SVM + HOG Features / Color-Shape-Texture      | Handcrafted feature extraction (HOG, color, texture) with classical ML                | 90–95% accuracy (small datasets), 94.7% multi-class recognition | General insect classification, baseline comparisons                 | 2023 | Huang et al. 2023 – Research on intelligent insect species identification based on computer vision – [Link](./papers/2023-Huang-insect-detection-SVM+HOG.pdf) |
| **other-CNN-based(except YOLO)**                 | Faster R-CNN + EfficientNet-B7                | EfficientNet backbone with region proposal networks for precise detection             | 99% / 96% / 93% (IP102, 5/10/15 classes), mAP 0.689             | Multi-class pest recognition (IP102), oilseed rape, field detection | 2022 | Kundur & Mallikarjuna 2022 – Insect Pest Image Detection and Classification using Deep Learning [Link](./papers/2022-Niranjan-insect-detection-CNN.pdf)|
| **YOLO-based**                | YOLOv8–v11 + Attention Modules (CBAM / ECA)   | Real-time multi-scale detection with attention mechanisms and small-object optimization | 78–89% mAP@0.5, 62–78% mAP@0.5:0.95, real-time (15–140 FPS)     | Rice pests, green peach aphids, cotton, real-time monitoring        | 2023,2024 | Tang et al. 2023 – *Improved Pest-YOLO with CBAM/ECA* [Link](https://www.sciencedirect.com/science/article/abs/pii/S1574954123003692) <br> Zheng et al. 2024 – *Rice-YOLO with Deep Supervision* [Link](./papers/2024-Zheng-insect-detection-YOLO.pdf) <br> Wang et al. 2025 – AMS-YOLO (YOLOv8n+attention)[Link](./papers/2025-Leilei-insect-detection-AMS-YOLO.pdf)|
| **Transformer-based**         | Vision Transformers (ViT) / DETR / GNViT      | Self-attention mechanisms for crop pest and camouflage detection with high accuracy   | 99.6% accuracy (Swin ViT), DETR achieving 75+ AP on locusts     | Groundnut pests, mosquito classification, camouflaged locusts       | 2024,2025 | Venkatasaichandrakanth et al. 2024 – *GNViT* [Link](./papers/2024-Venkata-insect-detection-Transformer.pdf) <br> Karim et al. 2024 – *Swin Transformer for Mosquito Classification* [Link](./papers/2024-Karim-insect-detection-Transformer.pdf) <br> Chen et al. 2025 – *Key-FG DETR for Locust Detection* [Link](./papers/2025-Chen-insect-detection-Transformer.pdf) |
| **Lightweight / Edge Models** | MobileNetV3 / YOLOv8n / Ultra-lightweight CNN | Parameter compression (<5M), on-device inference for edge deployment                  | ≥90% mAP@0.5, 98.6% accuracy, real-time on Raspberry Pi         | Mobile deployment, camera traps, IoT systems, smartphones           | 2024 | Sittinger et al. 2024 – *Insect Detect DIY Camera Trap* [Link](./papers/2024-Sittinger-insect-detection-Light.pdf) <br> GitHub: [maxsitt/insect-detect](https://github.com/maxsitt/insect-detect) <br> Yang et al. 2024 – *SRNet-YOLO for Tiny Pests* [Link](./papers/2024-Yang-insect-detection-Light.pdf) <br> *IoT-based Pest Monitoring* 2024 – [Link](./papers/2024-Jean-insect-detection-Light.pdf) |

---

**General Findings:**  
- YOLO and EfficientDet remain practical baselines for field use, balancing speed and accuracy.
- Transformers push accuracy further in lab and fine-grained contexts.
- Lightweight models (e.g., MobileNet, YOLO-Nano) are optimized for edge devices. No single method is best—model choice depends on deployment needs.
- Hybrid and open-set approaches are gaining ground for large-scale biodiversity applications.
