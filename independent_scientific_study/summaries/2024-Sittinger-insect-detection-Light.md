# Insect detect: An open-source DIY camera trap for automated insect monitoring
- **Authors:** Maximilian Sittinger, Johannes Uhler, Maximilian Pink, Annette Herz 
- **Year:** 2024
- **PDF:** [2024-Sittinger-insect-detection-Light](../papers/2024-Sittinger-insect-detection-Light.pdf)

---

## 1. Problem or Motivation
- Biodiversity studies require automated monitoring of insect populations (e.g., pollinators) at high spatiotemporal resolution.
- Traditional traps with manual counting are labor-intensive and often impractical for large-scale or long-term monitoring.
- This work introduces an open-source, low-cost “Insect Detect” DIY camera trap to continuously detect and classify insects visiting flowers.

## 2. Methodology
- The system is built from off-the-shelf hardware: a Raspberry Pi Zero 2 W with a Luxonis OAK-1 AI camera, plus solar power and environmental protection.
- On-device, a custom-trained YOLOv5 model performs real-time insect detection and tracking of insects landing on a fake flower platform.
- Detected insect images are then sent to a local computer where a second model classifies them into species or groups.
- The software and models are fully open-source, and the trap is designed to run autonomously in the field (solar-powered, temperature and humidity resistant) for entire seasons.

## 3. Datasets and Experiments
- The team created a dataset of insect images by deploying traps in a field setting (flower-visiting insects on a blue artificial flower).
- They trained the detection model on a combination of public insect images and their own data, and the classification model on a curated set of species images.
- Field trials were conducted to evaluate the system’s robustness and accuracy over time, comparing automated counts/classifications to manual observations.

## 4. Results and Findings
- The on-device YOLOv5 detector reliably detected and tracked insects in real time, enabling estimation of insect visitation rates (activity) after post-processing the timestamps.
- The system proved field-hardy – running continuously through hot and humid conditions without failure.
- The classification model achieved high top-1 accuracy on a test dataset and generalized well to real-world images captured by the trap, indicating that the two-stage approach (local detection + offline classification) is effective.
- Overall, the camera trap successfully recorded insect visit data autonomously, and its design can be adapted to other monitoring scenarios by swapping models or tweaking hardware.

## 5. Relevance to Insect Detection
- Represents a complete practical application of insect detection: from hardware to model deployment.
- For a thesis focusing on insect monitoring, this provides a blueprint of integrating a lightweight detector in the field.
- It also highlights challenges like edge computing limits (hence using a tiny Pi-compatible model), need for weather-proofing, and data management – all relevant if one plans to deploy insect detectors outside the lab.

## 6. Limitations and Future Work
- The current design targets insects that land on a specific platform, which may bias the sample (e.g., only certain pollinators). 
- The classification is done off-device, meaning real-time species identification isn’t instantaneous (though detection is).
- Also, only one artificial flower was used, which may not attract all insect types. 
- Future improvements include expanding to multiple trap units for larger coverage, integrating on-device classification as hardware improves, and extending to additional behaviors (e.g., flying insect detection without needing a landing platform).

## 7. Evaluation
- **Priority:** High. (Demonstrates real-world deployment of insect detection, bridging theory and practice.)
- **Use for Thesis:** Yes. (Great for citing an application example, and possibly for inspiration if building or evaluating similar systems for insect surveillance.)
