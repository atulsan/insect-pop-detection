# RF-DETR Object Detection vs YOLOv12 : A Study of Transformer-based and CNN-based Architectures for Single-Class and Multi-Class Greenfruit Detection in Complex Orchard Environments Under Label Ambiguity.
- **Authors:** Ranjan Sapkotaa, Rahul Harsha Cheppally, Ajay Sharda, Manoj Karkee
- **Year:** 2025
- **PDF:** [2025-Ranjan-object-detection-RF-DETR](../papers/2025-Ranjan-object-detection-RF-DETR.pdf)

---

## 1. Problem or Motivation
- Address single and multi class green fruit detection in orchards under occlusion, camouflage, and label ambiguity, by comparing a Transformer-based detector (RF-DETR) with a CNN-based YOLOv12 model.

## 2. Methodology
- Developed a custom orchard dataset with single class (all green fruits) and multi-class labels (occluded vs. visible fruits). RF-DETR uses a DINOv2 backbone with deformable attention for global context, whereas YOLOv12 relies on CNN feature pyramids for fast local feature extraction.

## 3. Datasets and Experiments
- The RFDETR and YOLOv12 variants were trained on the new dataset and evaluated on cluttered orchard images. 
- Single-class and occlusion-class experiments tested each model’s ability to detect fruits under varying visibility conditions

## 4. Results and Findings
- RF-DETR achieved mAP@50 = 0.9464 in single-class fruit detection, outperforming all YOLOv12 variants in localization. 
- In multi-class (occlusion) detection, RF-DETR also led with mAP@50 = 0.8298, while a YOLOv12 model had the highest mAP@50:95 (0.6622).
- RF-DETR showed faster convergence (~10 epochs) and more robust detection of partially occluded fruits

## 5. Relevance to Insect Detection
- Demonstrates advantages of Transformers for detecting objects in complex natural scenes with occlusion and camouflage. 
- Similar techniques could improve insect detection in foliage by leveraging global context to spot partially hidden insects.

## 6. Limitations and Future Work
- The study is domain-specific (green fruits in orchards), so generalization to small insects or other environments isn’t confirmed.
- Future work could apply RF-DETR to insect datasets and optimize it for smaller object sizes and edge deployment (as YOLO excels in speed).

## 7. Evaluation
- **Priority:** High (Key insight into Transformer vs CNN detectors in the wild.) 
- **Use for Thesis:** Yes (Valuable for discussing state-of-the-art object detectors’ trade-offs relevant to insect vision applications.)
