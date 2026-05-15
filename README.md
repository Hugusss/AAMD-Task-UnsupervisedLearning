# Unsupervised Learning Benchmark: Topological Analysis & Clustering

![Python](https://img.shields.io/badge/Python-3.11-blue.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Enabled-orange.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg)
![License](https://img.shields.io/badge/License-Academic-lightgrey.svg)

## 📌 Executive Summary
This repository contains a comprehensive academic benchmark of **Unsupervised Machine Learning** algorithms. The primary objective is to analyze, project, and cluster high-dimensional data, rigorously comparing the mathematical behavior, inductive biases, and geometric limitations of various models against known (but completely hidden during inference) ground-truth topologies.

## 📊 Datasets
The benchmark is conducted on two distinct vector spaces to test algorithm robustness across different spatial topologies:

* **Real Dataset:** 333 patterns, 5 continuous physical variables. Highly linear topology with dense, well-separated convex clusters.
* **Synthetic Dataset:** 360 patterns, 4 continuous variables. Characterized by complex, non-linear manifolds.

> **Note on Pre-processing:** Both datasets undergo rigorous Z-score standardization ($`z = \frac{x - \\mu}{\\sigma}`$) to ensure distance-based metrics (like Euclidean distance) and variance maximization algorithms operate without magnitude bias.

---

## ⚙️ Implemented Algorithms & Trajectory

### 1. Principal Component Analysis (PCA)
* **Role:** Linear dimensionality reduction and variance analysis.
* **Findings:** Successfully captured ~85% of variance in the Real dataset within 2 components, yielding highly separable clusters. However, it suffered a catastrophic information loss (~55% variance retained) on the Synthetic dataset, empirically proving the presence of non-linear structures.

### 2. t-Distributed Stochastic Neighbor Embedding (t-SNE)
* **Role:** Non-linear manifold learning and local topology preservation.
* **Findings:** A grid search over the `perplexity` hyperparameter successfully "unrolled" the complex geometries of the Synthetic dataset (revealing concentric rings and sine waves) that PCA had collapsed, proving its superiority for non-linear data visualization.

### 3. K-Means Clustering
* **Role:** Centroid-based, isotropic clustering.
* **Evaluation:** Extrinsic validation using the **Adjusted Rand Index (ARI)** across a search space of $K \\in [2, 8]$.
* **Findings:** K-Means achieved strong results on the convex Real dataset (ARI ~0.64). However, due to its inductive bias assuming spherical clusters, it failed entirely on the Synthetic dataset (ARI < 0.3), arbitrarily fracturing continuous non-linear manifolds.

### 4. Agglomerative Hierarchical Clustering (AHC)
* **Planned:** UPGMA and Complete Linkage dendrogram construction using Euclidean distance matrices.

### 5. Autoencoders & Self-Organizing Maps (SOM)
* **Planned:** Neural network-based non-linear projections and topological mapping via U-matrices.

---

## 🛠️ Environment & Requirements

This project is developed to run consistently inside an isolated Docker container environment to guarantee eproducibility.
### Dependencies
* `python >= 3.11.6`
* `numpy`
* `pandas`
* `scikit-learn`
* `matplotlib`
* `seaborn`
