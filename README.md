## Details
This project uses two object detection models: **(1) Faster R-CNN** and **(2) YOLOv11** for comparative analysis.

This project evaluates both models based on **accuracy (mAP)**, **inference speed (FPS)**, and **model size**.

---


##  Models Implemented

### 1️ Faster R-CNN (Two-Stage Detector)
- Custom CNN backbone
- Region Proposal Network (RPN)
- ROI Pooling
- Separate classification & regression heads
- High localization accuracy

### 2️ YOLO (One-Stage Detector)
- Single forward-pass detection
- Grid-based object prediction
- Joint localization & classification
- Optimized for real-time inference

---

##  Dataset
- **Link:** [DataSet Link](https://universe.roboflow.com/yolo-do-it-yhopz/helmet-detector-9rzmg-bmd6q)
- **Type:** for (a) Faster R-CNN used COCO format dataset (b) YOLO model used YOLOv11 format dataset
- **Classes:** 13 object categories
- **Annotations:**  
  - Faster R-CNN → COCO JSON format
  - YOLO → YOLO TXT format
- **Split:**  
  - Train: 70%  
  - Validation: 20%  
  - Test: 10%

---

## 🔄 Data Augmentation

To improve model robustness and generalization, a carefully designed data augmentation pipeline was applied using **Albumentations**.  
The augmentations were selected to simulate realistic camera motion, lighting variations, and mild blur conditions commonly observed in real-world video streams.

### Applied Augmentations
- **Shift, Scale, and Rotation**  
  Simulates minor camera movement and object displacement.
  - Shift limit: ±5%
  - Scale limit: ±8%
  - Rotation limit: ±5°
  - Probability: 0.7

- **Motion Blur**  
  Mimics motion-induced blur in video frames.
  - Blur kernel limit: 5
  - Probability: 0.3

- **Gaussian Blur**  
  Applies mild smoothing to reduce overfitting to sharp edges.
  - Kernel size: 3–5
  - Probability: 0.2

- **Random Brightness & Contrast**  
  Handles illumination changes across different environments.
  - Brightness limit: ±15%
  - Contrast limit: ±15%
  - Probability: 0.3

- **CLAHE (Contrast Limited Adaptive Histogram Equalization)**  
  Enhances local contrast under poor lighting conditions.
  - Clip limit: 2.0
  - Tile grid size: 8×8
  - Probability: 0.1 (applied sparingly)

---

## ⚙️ Training Configuration
1. **YOLO**

| Parameter | Value |
|--------|------|
| Learning Rate | 0.001 |
| Batch Size | 16 |
| Epochs | 100 |
| Training | Transfer Learning on Custom dataset |
| Hardware | GPU |

1. **YOLO**

| Parameter | Value |
|--------|------|
| Learning Rate | 0.0025 |
| Batch Size | 125 |
| Epochs | 2000 |
| Training | Transfer Learning on Custom dataset |
| Hardware | GPU |

---

## 📊 Evaluation Metrics
- **mAP (Mean Average Precision)**
- **Inference**
- **Model Size (MB)**

---

## 📈 Results

### 🔢 Quantitative Comparison

| Model | mAP (%) | mAP50 (%)| Inference | Model Size |
|-----|--------|-----|-----------|-----------|
| Faster R-CNN | 54.78 |74.96 | 0.1166 s/iter | 334 MB |
| YOLO | 92.8 | 88.5 |32 FPS | 5.23 MB |

> ⚠️ Results may vary depending on hardware and dataset size.

---

###  Qualitative Observations
- Faster R-CNN produces tighter bounding box and more stable output but very heavy and complex model
- YOLO is not perform better in real time but simple to write code and very light weight

---





