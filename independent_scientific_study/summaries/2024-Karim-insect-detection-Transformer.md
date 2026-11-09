# Advanced vision transformers and open-set learning for robust mosquito classification: A novel approach to entomological studies
- **Authors:** Ahmed Akib Jawad Karim, Muhammad Zawad Mahmud, Riasat Khan
- **Year:** 2024
- **PDF:** [2024-Karim-insect-detection-Transformer](../papers/2024-Karim-insect-detection-Transformer.pdf)

---

## 1. Problem or Motivation
- Mosquito surveillance requires not only classifying known species but also identifying when an input is not a known species (open-set) – e.g., a non-target insect or new species might appear in traps.
- This work addresses robust mosquito species classification using state-of-the-art transformers while incorporating open-set recognition to avoid misclassifying unknown inputs.

## 2. Methodology
- A Swin Transformer model and a lightweight MobileViT model were trained to classify 10 mosquito species from images.
- Extensive data augmentation and preprocessing were applied to improve feature learning.
- For open-set detection, they used the OpenMax algorithm with Weibull distribution modeling of activation vectors.
- Essentially, after the model outputs scores, OpenMax adjusts the probabilities to include an “unknown” class if the input’s feature distances are far from any known class centroids.
- They also compared a classic CNN (Xception) in the open-set scenario.

## 3. Datasets and Experiments
- A dataset of mosquito images covering 10 species was compiled (likely including both lab images and field photographs, possibly thousands of images in total).
- The models were tested in two settings: closed-set (all test images belong to the 10 trained species) and open-set (test images include some samples of species or objects not seen during training – e.g., other insects or even human images)
- Metrics included classification accuracy and F1-score for closed-set, and accuracy/F1 in recognizing known vs unknown for the open-set case.

## 4. Results and Findings
- The Swin Transformer achieved 99.60% accuracy (F1 = 0.996) in closed-set mosquito species classification, showing excellent performance.
- The MobileViT, despite being much smaller, also reached ~98.90% accuracy, indicating it’s nearly as effective with far fewer parameters.
- Under open-set evaluation, interestingly, a traditional Xception CNN slightly outperformed the advanced transformers in correctly handling unseen classes – i.e., Xception had higher accuracy/F1 when the task included rejecting unknown inputs.
- This suggests that the transformers, while extremely good at known-class discrimination, may produce overly confident predictions for unknowns, whereas Xception’s features were easier to calibrate with OpenMax for novelty detection.
- The framework still successfully detected when completely different insects or even human images were fed in, significantly enhancing practicality for real deployments (where non-mosquito images might get into traps or cameras).

## 5. Relevance to Insect Detection
- This work pushes the envelope in accuracy for insect classification (99.6% for mosquitoes is state-of-art) and importantly introduces the concept of open-set recognition to entomology.
-  In real-world insect monitoring, encountering species that a model wasn’t trained on is common; the ability to flag “unknown insect” instead of misidentifying it is crucial (for example, not mistaking a non-vector insect for a mosquito in disease surveillance).
- This makes the system far more robust for practical use.

## 6. Limitations and Future Work
- The models were trained on clear images of individual mosquitoes – performance might drop on cluttered backgrounds or partial images (the paper focused on classification of isolated specimens).
- The open-set handling, while effective, still saw the transformers lag behind a CNN for novel inputs; future research could combine transformer feature extraction with specialized open-set recognition layers or use few-shot learning to incorporate new classes. 
- Also, expanding to more than 10 species (there are hundreds of mosquito species of interest) and including other insect types in open-set testing would further validate the approach.

## 7. Evaluation
- **Priority:** Medium. (High significance for mosquito surveillance, but scope is narrower – classification vs. detection – and highly specialized.)
- **Use for Thesis:** Maybe. (Great if discussing classification accuracy or open-set issues; otherwise might be beyond the thesis scope if focusing on general detection.)