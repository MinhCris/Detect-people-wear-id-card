# AI-Based Employee ID Card Detection System

A two-stage computer vision system for automatically detecting whether employees are wearing ID cards and lanyards in workplace environments. The system combines YOLOv8 for person detection and YOLOv11 for small-object detection (ID card + lanyard).

---

## 📌 Overview

This project provides an automated ID card compliance monitoring solution using:

- **YOLOv8n** → Person Detection  
- **YOLOv11m** → ID Card & Lanyard Detection  

It is designed for real-world deployment in offices, factories, or workplaces where security and compliance are required.

This project was developed as part of a Bachelor Thesis at  
**University of Science and Technology of Hanoi (USTH)**.

---

## 🚀 Features

- Real-time person detection from video streams  
- Accurate ID card & lanyard recognition  
- High-performance YOLOv11 architecture  
- Bounding-box filtering to avoid incorrect matches  
- Supports both images and surveillance videos  
- High accuracy on real-world test data

---

## 🏗 System Architecture

### **Stage 1 — Person Detection (YOLOv8n)**
- Detects people in the full frame
- Extracts Region of Interest (ROI) for each person
- Lightweight and real-time

### **Stage 2 — ID Card & Lanyard Detection (YOLOv11m)**
- Receives the cropped person ROI  
- Detects:  
  - `id_card`  
  - `lanyard`  
- Classifies each person as:
  - **Compliant** (card/lanyard detected)
  - **Not compliant**

---

## 📦 Dataset

A custom dataset was built using surveillance camera footage (720p, 30 FPS) from CMC ATI.

| Item | Quantity |
|------|----------|
| Total labeled images | 1,426 |
| Total lanyard boxes | 1,306 |
| Total id-card boxes | 1,210 |
| Train / Validation split | 85% / 15% |

### **Data Augmentation**
- Mosaic  
- RandAugment  
- Gaussian noise  
- JPEG compression  
- Color jitter  
- Grayscale conversion  

---

## ⚙️ Training Configuration

### YOLOv11m Training Parameters

| Parameter | Value |
|----------|--------|
| Image size | 640×640 |
| Batch size | 8 |
| Epochs | 70 |
| Learning rate | 0.001 |

### Additional Rule  
A bounding-box filtering method removes predictions if the detected object is **too far from the person’s center** (over 30% distance), preventing mismatches in crowded scenes.

---

## 📊 Results

### **Training Metrics**
- Precision: **~0.95**  
- Recall: **~0.95**  
- F1-score optimal at confidence **0.484**  
- mAP50: **~0.97**  
- mAP50–95: **~0.72**

 
---

## 🛠 Installation & Usage

### 1. Install dependencies
```bash
pip install ultralytics opencv-python numpy
