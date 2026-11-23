# Waste Detection System Using YOLOv8
### AIRI Team – PITB AI Internship | Task 1

## 🚀 Live Demo

Try the deployed application:

**[Open Waste Detection App on Hugging Face Spaces](https://huggingface.co/spaces/SShehryarBurney/yolov8-waste-detection)**

## Overview

This project implements and evaluates an object detection pipeline for controlled waste material identification and sorting inspection across five supervisor-approved material categories (`cardboard`, `glass`, `metal`, `paper`, and `plastic`). The `BIODEGRADABLE` category was excluded from the project scope.

This pipeline is intended for controlled material-identification and sorting inspection scenarios, and is not designed for outdoor street litter detection, CCTV surveillance, or moving conveyor belts.

## Target Classes

- `0`: `cardboard`
- `1`: `glass`
- `2`: `metal`
- `3`: `paper`
- `4`: `plastic`

## Dataset & Annotation

- **Source**: 300 images from `GARBAGE CLASSIFICATION 3` v2 (Kaggle / Roboflow Universe, licensed under CC BY 4.0), with 416x416 RGB source images resized to `imgsz=640` during training.
- **Split**: 70% / 20% / 10% (`210` train, `60` validation, `30` test) with `1,043` valid YOLO bounding boxes (`metal`: 245, `cardboard`: 218, `plastic`: 207, `glass`: 204, `paper`: 169).
- **Annotation Practice**: Per supervisor clarification allowing a pre-annotated dataset and recommending at least 10 manually annotated images for practice, a separate 10-image manual annotation exercise was completed in Roboflow on 19 Nov 2026 and kept separate from the 300-image dataset.

## Training & Evaluation Summary

Both models were trained for 30 epochs with `imgsz=640`, `batch=8`, and `pretrained=True` on an NVIDIA Tesla T4 GPU using `ultralytics` (`8.4.216`).

### Validation Metrics (60 images, 323 instances)

- **YOLOv8n (`yolov8n_baseline`)**: Precision = `0.311` | Recall = `0.238` | mAP@0.5 = `0.207` | mAP@0.5:0.95 = `0.143`
- **YOLOv8s (`yolov8s_baseline`)**: Precision = `0.358` | Recall = `0.219` | mAP@0.5 = `0.213` | mAP@0.5:0.95 = `0.154`

### Test Metrics (30 images, 94 instances)

- **YOLOv8n (`yolov8n_test_evaluation`)**: Precision = `0.349` | Recall = `0.422` | mAP@0.5 = `0.350` | mAP@0.5:0.95 = `0.224`
- **YOLOv8s (`yolov8s_test_evaluation`)**: Precision = `0.689` | Recall = `0.297` | mAP@0.5 = `0.397` | mAP@0.5:0.95 = `0.280`

## Inference & Error Analysis

- Batch inference was run on all 30 unseen test images at `conf=0.35` with bounding boxes, class labels, and confidence scores saved to `outputs/predictions/yolov8n_test_predictions` and `outputs/predictions/yolov8s_test_predictions`.
- A manual error analysis of 10 weak or incorrect test predictions was completed alongside improvement recommendations covering diverse training examples for difficult/crowded items, targeted label auditing on confirmed issues, and controlled model comparison.

## Repository Contents

- **Project Notebook**: Complete implementation and experimentation.
- **Project Report**: Detailed documentation of the project methodology, training, evaluation, and findings. (`report/final_report.pdf`)

## Technologies Used

- Python
- Ultralytics YOLOv8
- PyTorch
- Google Colab
- Roboflow
- Hugging Face Spaces
