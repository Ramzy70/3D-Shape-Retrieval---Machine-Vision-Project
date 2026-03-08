# 3D Shape Retrieval Pipeline (ModelNet10) 📐

A complete view-based 3D shape retrieval system that extracts semantic embeddings from 3D meshes using a multi-view CNN architecture.

## 🚀 Project Overview
This project implements a full pipeline for retrieving 3D objects based on visual similarity. Due to hardware limitations, the project includes significant optimizations in mesh processing and rendering efficiency.

* **Dataset:** ModelNet10 (3D mesh files in `.off` format).
* **Approach:** View-based retrieval using 2D projections of 3D objects.
* **Key Challenge:** Balancing computational load with model depth using mesh simplification and resolution scaling.

## 🛠 Technical Implementation

### 1. Multi-View Rendering Strategy
To create robust 3D descriptors, each mesh undergoes a transformation pipeline:
* **Mesh Normalization:** Translation to origin and scaling to a unit sphere for consistent camera distancing.
* **Quadric Decimation:** Meshes simplified to a maximum of 500 faces to reduce memory overhead.
* **Consistent Viewpoints:** 8 fixed camera poses (azimuth/elevation) capture a comprehensive visual profile.

### 2. Retrieval Backbone
* **ViewEncoder:** A custom CNN extracts 128D embeddings from each of the 8 views.
* **Aggregation:** Simple average pooling across view embeddings to create a single global shape descriptor.
* **Classification Head:** Linear layer for training with Cross-Entropy loss.

## 📊 Results & Metrics
Despite severe computational constraints requiring a reduced dataset (5% training, 10% test) and low-resolution (32x32) renders, the pipeline successfully implements the retrieval logic:

| Metric | Value |
| :--- | :--- |
| **Final Train Accuracy** | 0.505 |
| **Mean Average Precision (mAP)** | 0.3143 |
| **Precision @ 10** | 0.3012 |

## 🛠 Requirements
* `trimesh` for mesh processing.
* `torch` & `torchvision` for the deep learning backbone.
* `matplotlib` for 2D rendering from 3D scenes.
* `Xvfb` for headless rendering in server environments.
