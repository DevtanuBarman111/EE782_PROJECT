# EE782 Project – Replicating 'Deep Learning with Sparse Representations for Biomedical Signals' with Extensions to CWT-based fECG Detection and DWT-UNet MRI Segmentation

This repository contains our EE782 course project at **IIT Bombay**, based on replicating and extending the paper:

> **N. Lakshmisha et al., "Deep Learning with Sparse Representations for Biomedical Signals", ICMOCE 2023.**

We implement and study wavelet–deep learning hybrids for:
- **CWT-based fetal ECG (fECG) detection** from abdominal ECG
- **DWT-UNet based skull stripping** in brain MRI
- **Multiresolution K-means GM/WM segmentation**
- **Benchmarking framework** for performance vs. model complexity

---

## Project Components

### 1. Fetal QRS Detection (CWT + CNN)
- Dataset: ADFECGDB (abdominal + direct fetal ECG)
- Preprocessing: DC removal, normalization, 270 ms windows
- Time–frequency representation: CWT scalograms (`128×128×3`)
- Model: MobileNetV2 backbone with custom head
- Test performance (on 500-window subset):
  - Accuracy: **96.0%**
  - Precision: **97.62%**
  - Recall: **95.35%**
  - F1-score: **96.47%**

---

### 2. Brain MRI Skull Stripping (DWT-UNet vs UNet)
- Synthetic 2D MRI-style dataset (256×256)
- Models:
  - **DWT-UNet**: Haar DWT used instead of max-pooling, IDWT for upsampling
  - **Vanilla UNet**: same channels, standard pooling/upsampling
- Both have ~**487k parameters**

Test performance (synthetic data):
- DWT-UNet: Dice ≈ **99.4%**, IoU ≈ **98.8%**
- UNet: Dice ≈ **99.9%**, IoU ≈ **99.8%**

---

### 3. GM/WM Segmentation via Multiresolution K-means
- Apply Haar DWT up to level 5 on skull-stripped slices
- Run K-means on LL5 → propagate centroids to finer scales
- Obtain GM / WM / background segmentation

---

### 4. Benchmarking Framework

We compare:
- Classification metrics (accuracy, precision, recall, F1)
- Segmentation metrics (Dice, IoU)
- Model size (parameters)
- Rough computational load (FLOPs, estimated)

Notebooks:
- `notebooks/Part3_Benchmarking.ipynb`

---

## Report

The full IEEE-style report (prepared for EE782) is:

- `EE782_REPORT.pdf`
This report includes:
- Detailed methodology
- All plots and visualizations
- Comparison with the original paper
- Discussion and future directions

---

## Authors (IIT Bombay)

- **Devtanu Barman** (Roll No. 22B3904)  
- **Sanjay Meena** (Roll No. 22B3978)  
- **Sarthak Niranjan** (Roll No. 22B3923)  

Department of Electrical Engineering,  
Indian Institute of Technology Bombay.

---

## How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/EE782-DeepSparseBioSignals.git
   cd EE782-DeepSparseBioSignals
