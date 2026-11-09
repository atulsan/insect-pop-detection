# AI and IoT-powered edge device optimized for crop pest and disease detection
- **Authors:** Jean Pierre Nyakuri, Celestin Nkundineza, Omar Gatera, Kizito Nkurikiyeyezu, Gervais Mwitende
- **Year:** 2024
- **PDF:** [2024-Jean-insect-detection-Light](../papers/2024-Jean-insect-detection-Light.pdf)

---

## 1. Problem or Motivation
- Surveys the state-of-the-art deep learning algorithms for pest and disease detection in the context of Internet of Things (IoT)-based agriculture. 
- With smart farming on the rise, there’s a need to summarize current methods and identify gaps for deploying AI pest detection on distributed sensors and devices.

## 2. Methodology
- This comprehensive review analyzes and compares recent models (2019–2024) for insect pest detection and classification, including CNN-based approaches (ResNet, EfficientDet, Faster R-CNN, etc.) and emerging Transformer-based and hybrid models.
- It also examines how these models are adapted to edge devices, discussing techniques like model quantization, pruning, and lightweight network design for IoT.
- The review covers over 150 references, highlighting each model’s architecture, the dataset used, performance metrics, and deployment considerations.

## 3. Datasets and Experiments
- Common public pest datasets (IP102, D0, Rice Pest datasets, etc.) are summarized in terms of size and usage. 
- The paper compiles reported results of various models on these datasets, enabling a side-by-side performance comparison.
- For example, it notes mobile-integrated YOLO models achieving up to 99% accuracy on certain tasks and specialized models like YOLO-PPLC Bot (an improved YOLOv5 for pests) attaining 95.3% mAP.
- It also catalogues issues such as class imbalance and the difficulty of detecting tiny pests, which many papers address via data augmentation or attention modules.

## 4. Results and Findings
- The review finds that deep learning models have dramatically improved pest detection accuracy, with some achieving near-perfect scores in controlled settings.
- For instance, deploying YOLO models on mobile devices has yielded up to ~99% accuracy in certain experiments.
- However, it emphasizes persistent challenges: very small pests and overlapping insects remain hard to detect reliably for even the best models, due to limited resolution and the nature of bounding boxes.
- It also notes a trend towards lightweighting – many recent works introduce lightweight detectors or efficient networks (Tiny-YOLO variants, MobileNets, etc.) to better balance accuracy and computational cost for IoT deployment.
- Furthermore, the review highlights the importance of open-set recognition and incremental learning in pest management, because new pest species or conditions can emerge in real-world deployment.

## 5. Relevance to Insect Detection
- This review is highly relevant as a summary of the field’s progress, making it easier to spot which techniques consistently work best for insect detection.
- It identifies key models to consider (e.g., YOLOv8x fine-tuned for pests, Transformer models for small object detection) and also pinpoints gaps like the need for better small-object detection and generalization.
- For someone formulating a thesis, the review provides an invaluable big-picture view and justification for why their chosen approach addresses an open problem.

## 6. Limitations and Future Work
- As a review, it doesn’t introduce new experiments, but it calls for future research into areas like few-shot learning for emerging pests, integration of multi-spectral sensors (not just RGB images) to catch pests that are invisible in certain spectra, and more robust deployment strategies for varying field conditions (lighting, weather).
- It also suggests that combining techniques (e.g., classical traps + AI, or multi-modal data like imagery plus pheromone sensor triggers) could yield the next breakthroughs.

## 7. Evaluation
- **Priority:** High. (Consolidates knowledge and provides context crucial for understanding where novel contributions can be made.)
- **Use for Thesis:** Yes. (Use it to support problem statements and to compare the thesis approach with existing works, as well as to cite performance figures and consensus views in the literature.)
