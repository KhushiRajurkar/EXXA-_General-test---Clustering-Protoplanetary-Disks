# 🌌 ML4Sci GSoC Test Task — Clustering Protoplanetary Disks

This repository contains my completed general test task submission for the ML4Sci Google Summer of Code 2025. The goal of the task is to perform **unsupervised clustering** on synthetic continuum observations of protoplanetary disks (1250 microns) and analyze their morphological structures.

These synthetic FITS files simulate realistic ALMA observations generated through hydrodynamics and radiative transfer simulations. The challenge involves identifying meaningful groupings (e.g., gaps, rings, planet-induced spirals) without using any labels.

---

## Models Implemented

The notebook explores **four clustering pipelines** and selects a final model based on performance, interpretability, and generalization across disk morphologies:

### ✅ 1. **Improved KMeans Clustering (Final Model)**
- Resizes disks to 300×300 for efficiency.
- Uses standardized pixel intensities and applies KMeans clustering (k=5).
- Provides **fast and visually accurate** segmentation of disk features like gaps and spirals.
- Batch processes and saves `.png` results.
- Model saved with `joblib` as improved_kmeans_model.pkl.

CLustering results saved in: [`clustering_kmeans_raw/`](https://drive.google.com/drive/folders/1AFfx9Tu9jJ3qBM7exEAxFZhFY-1saN7u?usp=drive_link)

---

### 2. **PCA + Patch-based KMeans (Exploratory)**
- Extracts local image patches (10×10), flattens, standardizes, and applies PCA.
- Clustering is done on reduced PCA components.
- Captures morphology-aware features, especially useful for subtle structures.
- Includes optional silhouette-based `auto_choose_k`.
- More sensitive to structure but less robust across all disks.

Results saved in: [`clustering_results/`](https://drive.google.com/drive/folders/1NHKf3KppMx5mLPN2QrDlVVx3a62qRMqS?usp=drive_link)

---

### 3. **Gaussian Mixture Models (GMM)**
- Uses `GaussianMixture` on standardized pixels.
- Allows soft clustering.
- Performance is dataset-dependent; sometimes unstable in noisy disks.

---

### 4. **HDBSCAN (Density-Based)**
- Preprocesses the disk image (cleaning NaNs/Infs, clipping, downsampling).
- Applies `HDBSCAN` with adjustable parameters.
- Capable of finding variable-density structures.
- Works well on some images, but inconsistent across the full dataset.

---

## Summary of Notebook Workflow

| Step | Description |
|------|-------------|
| 1 | Load `.fits` files from Drive |
| 2 | Visualize raw disk slices |
| 3 | Apply clustering algorithms |
| 4 | Evaluate results via visuals and silhouette |
| 5 | Save cluster maps to output folders |

---

## Final Model Decision

After evaluating all approaches, the **Improved KMeans** method was selected as the final model based on:

1) Structural clarity in rings, gaps, and spirals
2) Robustness across various disk shapes and viewing angles
3) Faster runtime and better visual interpretability
4) Clean output without needing extensive parameter tuning

---
