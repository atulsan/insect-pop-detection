# AMS-YOLO: multi-scale feature integration for intelligent plant protection against maize pests
- **Authors:** Leilei Deng,  Di Fang,  Aziz Ullah,  Qi Hou, Helong Yu
- **Year:** 2025
- **PDF:** [2025-Leilei-insect-detection-AMS-YOLO](../papers/2025-Leilei-insect-detection-AMS-YOLO.pdf)

---

## 1. Problem or Motivation
- Maize crops suffer from diverse pest species with similar morphologies and occur in cluttered field environments.
- Conventional detectors struggled with inter-species similarity and complex backgrounds, leading to missed detections.
- AMS-YOLO aims to enhance YOLO’s ability to detect maize pests across growth stages and crowded conditions.

## 2. Methodology
-  Built on YOLOv8n with three custom modules
    - SMCA attention : an attention mechanism to better highlight pest targets in complex backgrounds
    - MSBlock : a multi-scale feature fusion block to handle pests from larvae to adults
    - AMConv : an asymmetric convolutional downsampling module preserving fine details for similar-looking species
- These improvements were integrated into YOLOv8n, yielding AMS-YOLO (Attention + Multi-scale + optimized downSampling).

## 3. Datasets and Experiments
- Compiled a dataset of 13 common maize pest species covering all developmental stages (egg, nymph/larva, adult) for training and evaluation.
- Models compared include baseline YOLOv8n, SSD, RT-DETR, and other YOLO variants, tested on metrics like precision, recall, mAP@0.5, and mAP@0.5:0.95.

## 4. Results and Findings
- AMS-YOLO achieved 94.2% mAP@0.5 and 73.7% mAP@0.5:0.95 on the maize pest test set, outperforming the original YOLOv8n by +3.2% and +4.0% respectively.
- Precision (90.0%) and recall (89.8%) also improved ~3–4% over YOLOv8n.
- Notably, AMS-YOLO is extremely lightweight – the model is only 5.3 MB in size (≈20% smaller than YOLOv8n) with 19.6% fewer parameters, making it well-suited for edge devices.
- It outperformed SSD and faster RCNN-based models in both accuracy and speed, and ran successfully on a Jetson Nano with low resource usage.

## 5. Relevance to Insect Detection
- This work is directly aimed at pest insect detection in real field conditions, showing that targeted architectural tweaks can significantly boost a modern YOLO’s performance on small, similar-looking insects.
- It also emphasizes lightweight design, which is crucial for deploying detection models on farms via drones or edge IoT traps. The success of AMS-YOLO highlights the importance of multi-scale feature fusion and attention for insect tasks.

## 6. Limitations and Future Work
- The study focused on 13 pest species in maize; performance on a broader set of crops or non-maize pests remains untested.
- Also, while it’s efficient on a Jetson Nano, extremely low-power microcontrollers might still struggle without further model compression or quantization.
- Future work could generalize the method to more pest types (e.g., orchard pests) and incorporate temporal data from video for even better accuracy in tracking infestations.

## 7. Evaluation
- **Priority:** High. (Represents the cutting-edge for specialized insect pest detectors and balances accuracy and efficiency.)
- **Use for Thesis:** Yes. (Great case study for improving and deploying YOLO models in agricultural pest monitoring.)
