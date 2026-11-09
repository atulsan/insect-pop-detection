# Insect Pest Image Detection and Classification using Deep Learning
- **Authors:** Niranjan C Kundur, P B Mallikarjuna
- **Year:** 2022
- **PDF:** [2022-Niranjan-insect-detection-CNN](../papers/2022-Niranjan-insect-detection-CNN.pdf)

---

## 1. Problem or Motivation
- Reduce crop losses due to insect pests by using deep learning to automate pest detection, as manual scouting is time-consuming and error-prone.
- The authors note that over 40% of agri output is lost to pests globally, motivating improved pest monitoring tools.

## 2. Methodology
- Proposed two models based on Faster R-CNN with EfficientNet backbones (B4 and B7) for insect pest detection and classification.
- These models bring EfficientNet’s high feature representation capacity into the Faster R-CNN framework to improve accuracy on small pest objects.
- They fine-tuned these models on a public pest dataset, comparing against existing CNN models.

## 3. Datasets and Experiments
- Used the IP102 dataset (a large pest image dataset of 102 classes). To manage complexity, experiments were conducted on subsets of 5, 10, and 15 pest classes from IP102, evaluating model accuracy on each subset.  
- Performance metrics include classification accuracy of detected pests in each scenario.

## 4. Results and Findings
- The Faster R-CNN + EfficientNet-B7 model achieved 99.0%, 96.0%, and 93.0% average accuracy for 5, 10, and 15 pest classes respectively, outperforming the EfficientNet-B4 variant and other baseline models.
- It showed that a stronger backbone (B7) significantly boosts recognition of pests, even as the number of classes increases, while still maintaining reasonable inference speed (~19.5 FPS in tests, comparable to ~20.7 FPS of a smaller model).

## 5. Relevance to Insect Detection
- Demonstrates the benefit of combining state-of-the-art CNN backbones with region-based detectors for insect pests.
- Many insect detection tasks involve small objects (pests on leaves), and this work showed that high-capacity networks like EfficientNet can improve accuracy in such scenarios.
- It provides a strong baseline for pest detection before transformer models or one-stage YOLOs became prevalent.

## 6. Limitations and Future Work
- The evaluation was restricted to subsets of IP102, not the full 102 classes, raising questions about performance on a more diverse set. 
- Also, using Faster R-CNN means slower inference and more computation, which may limit field deployment on low-power devices.
- Future work might involve optimizing the model or using one-stage detectors for speed, and extending to real-world field images beyond the relatively clean laboratory images common in IP102.

## 7. Evaluation
- **Priority:** Medium (Important as a proof-of-concept of CNN-based pest detectors, though newer models have emerged since.)
- **Use for Thesis:** Maybe (Useful as background or baseline in a thesis on pest detection, but more modern approaches might take precedence.)
