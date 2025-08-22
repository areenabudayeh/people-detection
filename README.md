# Object Detection in Paintings Using Transfer Learning 

## Introduction
This project explores the problem of **detecting people in paintings**, which is more complex than natural scene detection due to variations in textures, colors, and artistic styles. Paintings deviate from real-world proportions, especially across diverse art styles.

We evaluate two state-of-the-art object detection models:
- **YOLOv8 (You Only Look Once):** A fast real-time object detector.
- **Faster R-CNN:** A two-stage detector known for high precision in cluttered scenes.

The goal was not only to test model performance but also to better understand how **computer vision models generalize to non-photorealistic art**.

---

## Dataset
We used a curated subset of the **PeopleArt dataset**, which contains annotated paintings across **27 unique art styles** such as Realism, Impressionism, Cubism, and Abstract Art.

- **Format:** Pascal VOC (XML), converted to YOLO format for YOLOv8  
- **Splits:**
  - Train: 70% (1011 images)
  - Validation: 20% (289 images)
  - Test: 10% (145 images)  
- **Classes:** 1 (person)

---

## YOLOv8 Model
### Model & Architecture
- Model: **YOLOv8m**
- Parameters: ~25.8M
- Layers: 169
- Fine-tuned using **transfer learning** (last 15 layers unfrozen).

### Training Configuration
- Epochs: 50  
- Batch size: 16  
- Image sizes: 896 / 1024  
- Optimizer: Adam (lr = 1e-4)  
- Early stopping with patience = 10  
- Augmentations: Copy-Paste, Mosaic, MixUp, random resizing, cropping.

---

## Faster R-CNN Model
### Model & Architecture
- Backbone: **ResNet-50 + Feature Pyramid Network (FPN)**  
- Region Proposal Network (RPN) with multiple anchor sizes/aspect ratios.  
- Two-stage detection (classification + regression).  

### Training Details
- Optimizer: AdamW  
- Augmentations: Random Erasing, Color Jitter  
- Normalization: COCO dataset stats  

---

## Conclusion
This project demonstrates how modern deep learning models can be adapted to the **unique domain of fine art**. While object detection has matured in natural image contexts, applying it to paintings reveals new challenges—such as **stylistic abstraction, symbolic representation, and non-standard human forms**.  

By fine-tuning YOLOv8 and Faster R-CNN with domain-aware augmentations, we explored how machine learning can bridge the gap between **computer vision and cultural heritage analysis**. Beyond raw performance, this project underscores the importance of adapting AI tools to **diverse visual domains** and opens the door for applications in **digital art studies, museum curation, and visual storytelling**.

This study highlights the challenges of applying deep learning models to **non-photorealistic domains** and suggests that **holistic, augmentation-rich models like YOLOv8** are more robust to such domain shifts.
