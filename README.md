# 3D Car Detection using LiDAR (KITTI Dataset)

This repository contains a complete end-to-end implementation of a 3D object detection pipeline using LiDAR point cloud data. The model follows a compact PointPillars-style architecture and is trained and evaluated on the KITTI dataset.

---

## Overview

This notebook implements the full pipeline required for 3D car detection:

* Parsing KITTI dataset (LiDAR + labels)
* Point cloud preprocessing and pillarization
* Feature encoding for voxelized pillars
* Training a lightweight PointPillars-like model
* Validation and checkpointing
* Inference on validation data
* KITTI-style mAP evaluation

The implementation is designed to be simple, modular, and easy to follow within a single notebook.

---

## Notebook

* `edited_3D_object_detection_notebook.ipynb`
  Contains the full implementation including data loading, preprocessing, training, and evaluation.

---

## Pipeline Details

### 1. Data Loading

* Reads KITTI LiDAR point clouds (`.bin`)
* Parses corresponding label files
* Splits dataset:

  * First 2000 frames → training
  * Next 200 frames → validation

### 2. Preprocessing (Pillarization)

* Converts raw point clouds into vertical columns (pillars)
* Encodes spatial features per pillar
* Caches processed data to improve training speed

### 3. Model

* Compact PointPillars-style architecture
* Includes:

  * Pillar feature encoder
  * Backbone network
  * Detection head for bounding box regression and classification

### 4. Training

* Trains on pillarized LiDAR data
* Tracks validation performance
* Saves best model checkpoint

### 5. Inference

* Runs detection on validation frames
* Outputs 3D bounding boxes

### 6. Evaluation

* Computes KITTI-style mean Average Precision (mAP)
* Evaluates detection performance on validation set

---

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Notebook

```bash
jupyter notebook edited_3D_object_detection_notebook.ipynb
```

Run all cells sequentially.

---

## Dataset

This project uses the KITTI 3D Object Detection dataset.

You need to download it manually and update paths inside the notebook.

Expected structure:

```
KITTI/
├── training/
│   ├── velodyne/
│   ├── label_2/
│   └── calib/
```

---

## Notes

* The implementation uses a reduced dataset subset for faster experimentation.
* Preprocessing results are cached to avoid recomputation.
* The model is intentionally lightweight for easier training on limited hardware.

---

## Future Improvements

* make the model more robust
* Full dataset training (beyond subset)
* Better backbone (e.g., SECOND / sparse convs)
* Data augmentation (rotation, scaling, flipping)
* Multi-class detection
* Visualization of 3D bounding boxes

---

