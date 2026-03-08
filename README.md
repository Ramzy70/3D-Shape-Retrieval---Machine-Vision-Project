# 3D Shape Retrieval Pipeline (ModelNet10) 📐

A complete view-based 3D shape retrieval system that extracts semantic embeddings from 3D meshes using a multi-view CNN architecture.

## 🚀 Project Overview
This project implements a full pipeline for retrieving 3D objects based on visual similarity. Due to hardware limitations, the project includes significant optimizations in mesh processing and rendering efficiency.

* [cite_start]**Dataset:** ModelNet10 (3D mesh files in `.off` format)[cite: 69, 71].
* [cite_start]**Approach:** View-based retrieval using 2D projections of 3D objects[cite: 78].
* [cite_start]**Key Challenge:** Balancing computational load with model depth using mesh simplification and resolution scaling[cite: 81, 87].

## 🛠 Technical Implementation

### 1. Multi-View Rendering Strategy
To create robust 3D descriptors, each mesh undergoes a transformation pipeline:
* [cite_start]**Mesh Normalization:** Translation to origin and scaling to a unit sphere for consistent camera distancing[cite: 79].
* [cite_start]**Quadric Decimation:** Meshes simplified to a maximum of 500 faces to reduce memory overhead[cite: 80, 776].
* [cite_start]**Consistent Viewpoints:** 8 fixed camera poses (azimuth/elevation) capture a comprehensive visual profile[cite: 82].

### 2. Retrieval Backbone
* [cite_start]**ViewEncoder:** A custom CNN extracts 128D embeddings from each of the 8 views[cite: 96].
* [cite_start]**Aggregation:** Simple average pooling across view embeddings to create a single global shape descriptor[cite: 97].
* [cite_start]**Classification Head:** Linear layer for training with Cross-Entropy loss[cite: 97, 98].

## 📊 Results & Metrics
[cite_start]Despite severe computational constraints requiring a reduced dataset (5% training, 10% test) and low-resolution (32x32) renders, the pipeline successfully implements the retrieval logic[cite: 89, 1120]:

| Metric | Value |
| :--- | :--- |
| **Final Train Accuracy** | [cite_start]0.505 [cite: 102] |
| **Mean Average Precision (mAP)** | [cite_start]0.3143 [cite: 111] |
| **Precision @ 10** | [cite_start]0.3012 [cite: 111] |

## 🛠 Requirements
* [cite_start]`trimesh` for mesh processing[cite: 140].
* [cite_start]`torch` & `torchvision` for the deep learning backbone[cite: 211].
* [cite_start]`matplotlib` for 2D rendering from 3D scenes[cite: 83].
* [cite_start]`Xvfb` for headless rendering in server environments[cite: 153].
