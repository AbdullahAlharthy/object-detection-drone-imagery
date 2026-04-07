# Object Detection in Drone Imagery

Academic project | University of Jeddah | Data Science Department | 2025

## Overview

Trained YOLOv8 and YOLO11 models on the VisDrone2019 dataset — one of the most challenging
aerial object detection benchmarks. Scaled training data from 6,471 to 12,942 images via
a custom augmentation pipeline. Best result: YOLO11l at 34.6% mAP@50 with 1.9ms inference.

## Results

| Metric | Score |
|--------|-------|
| Best mAP@50 | 34.6% |
| Best mAP@50-95 | 21.0% |
| Inference Speed | 1.9ms/image |
| Model | YOLO11l (190 layers, 25.3M params) |

## Training Experiments

| Run | Model | Epochs | mAP@50 | Notes |
|-----|-------|--------|--------|-------|
| train6 | YOLOv8n | 10 | 0.236 | Baseline |
| train4 | YOLOv8n | 20 | 0.250 | +6% from more epochs |
| train3 | YOLOv8m | 20 | 0.346 | Model scaling |
| train7 ★ | YOLO11l | 20 | 0.346 | Selected — best architecture + speed |

## Per-Class Results — YOLO11l

| Class | Precision | Recall | mAP@50 |
|-------|-----------|--------|--------|
| 🚗 car | 0.677 | 0.766 | 0.775 |
| 🚌 bus | 0.619 | 0.462 | 0.528 |
| 🚐 van | 0.453 | 0.451 | 0.441 |
| 🚶 pedestrian | 0.448 | 0.431 | 0.417 |
| 🏍️ motor | 0.496 | 0.415 | 0.409 |
| 🚛 truck | 0.471 | 0.356 | 0.357 |
| 👥 people | 0.566 | 0.245 | 0.314 |
| 🛺 tricycle | 0.415 | 0.287 | 0.269 |
| awning-tri | 0.260 | 0.179 | 0.150 |
| 🚲 bicycle | 0.151 | 0.225 | 0.103 |
| **all** | **0.437** | **0.351** | **0.346** |

## Data Augmentation Pipeline

Custom augmentation doubled training data from 6,471 to 12,942 images:

| Type | Technique |
|------|-----------|
| Geometric | HorizontalFlip ±50%, RandomRotation ±10°, Scale 0.5 |
| Visual | HSV hue 0.015, Saturation 0.7, Brightness 0.4 |

## Inference Speed Breakdown

| Stage | Time |
|-------|------|
| Preprocess | 0.1ms |
| Inference | 1.9ms |
| Postprocess | 0.7ms |
| **Total** | **2.7ms** |

## Dataset

**VisDrone2019** — aerial imagery benchmark captured by drone cameras across 14 cities in China.

Key challenges:
- Objects often under 10px in width
- Hundreds of overlapping instances per scene
- Severe class imbalance (cars dominate, bicycles rare)
- Varying altitudes and lighting conditions

## Tech Stack

| Category | Tools |
|----------|-------|
| Models | YOLO11l, YOLOv8m, YOLOv8n |
| Framework | PyTorch · Ultralytics |
| Processing | OpenCV · CUDA |
| Augmentation | Custom pipeline (ColorJitter, HorizontalFlip, RandomRotation, HSV) |

## Key Findings

- Data augmentation alone (train6 → train4) improved mAP by +6% with the same model
- Model scaling from YOLOv8n to YOLO11l pushed mAP from 0.250 to 0.346
- YOLO11l selected over YOLOv8m despite equal mAP — superior architecture depth and 1.9ms inference makes it deployable in real-time UAV systems
- Car detection achieved 77.5% mAP — strongest class due to dataset dominance
- Bicycle detection at 10.3% mAP — reflects extreme class imbalance challenge

## Team

University of Jeddah 2025
