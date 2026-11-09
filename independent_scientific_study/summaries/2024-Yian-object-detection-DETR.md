# DETRs Beat YOLOs on Real-time Object Detection
- **Authors:** Yian Zhao, Wenyu Lv, Shangliang Xu, Jinman Wei, Guanzhong Wang, Qingqing Dang, Yi Liu, Jie Chen
- **Venue/Year:** 2024
- **PDF:** [2024-Yian-object-detection-DETR](../papers/2024-Yian-object-detection-DETR.pdf)

---

## 1. Problem or Motivation
- Improve real-time object detection by overcoming YOLO’s speed-accuracy limitations due to NMS post-processing. 
- The goal is to design a Real-Time Detection Transformer (RT-DETR) that can rival or surpass YOLO in both speed and accuracy without needing NMS.

## 2. Methodology
- Proposed RT-DETR with a two-step design: 
    - an efficient hybrid Transformer encoder that decouples intra-scale and cross-scale attention to speed up multi-scale feature processing
    - an uncertainty-minimal query selection strategy to initialize DETR queries with high-confidence features, improving accuracy. The model allows flexible speed-accuracy trade-offs by adjusting decoder layers without retraining

## 3. Datasets and Experiments
- Evaluated on COCO (val2017) for standard object detection performance.
- Also tested scaled-down versions (S/M models) against YOLOv5/v7/v8 counterparts.
- Additionally pre-trained on Objects365 to gauge improvements with extra data.

## 4. Results and Findings
- RT-DETR achieves 53.1% AP on COCO at 108 FPS (ResNet-50 backbone), outperforming YOLOv8 L/X models in both accuracy and speed.
- A larger RT-DETR (R101) reaches 54.3% AP @ 74 FPS, and scaled-down RT-DETR variants also beat YOLO S/M models.
- Notably, RT-DETR-R50 outperforms DINO-Deformable-DETR by +2.2% AP and ~21× higher FPS.
- After additional training on Objects365, AP further improves to 55–56%

## 5. Relevance to Insect Detection
- Shows that Transformer-based detectors can be optimized for real-time performance, suggesting that future insect detectors could use similar end-to-end Transformer designs to avoid NMS and handle edge deployment scenarios efficiently.

## 6. Limitations and Future Work
- While closing the gap, RT-DETR still involves a heavier architecture than YOLO (due to Transformer components), which might be challenging on very low-power devices.
- Future work could explore even lighter backbones or apply RT-DETR to domain-specific tasks (e.g., pest detection) to validate its generalization and speed on smaller objects.

## 7. Evaluation
- **Priority:** High (Introduces a cutting-edge model that outperforms YOLO, relevant for next-gen detectors.)
- **Use for Thesis:** Yes (Provides state-of-art benchmarks and techniques directly applicable to designing fast insect detection models.)