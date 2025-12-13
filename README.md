
# DGHME: A Hierarchical Hybrid Expert Multi-task Learning Model for Disease Grouping

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Framework](https://img.shields.io/badge/PyTorch-1.8%2B-orange.svg)](https://pytorch.org/)

This repository contains the official implementation of the paper: **"DGHME: A Hierarchical Hybrid Expert Multi-task Learning Model for Disease Grouping in Diabetes Complication Prediction"**.

**DGHME** (Disease-Grouping Hierarchical Mixed Expert) is a novel multi-task learning framework designed to predict four major complications of Type 2 Diabetes Mellitus (T2DM): **Diabetic Retinopathy (DR)**, **Diabetic Nephropathy (DN)**, **Coronary Heart Disease (CHD)**, and **Fatty Liver Disease (FLD)**.

## 📖 Abstract

Accurate identification and prediction of diabetes complications are crucial for improving patient health. However, existing prediction models predominantly employ single-task learning (STL) paradigms, failing to fully leverage the intrinsic correlations among different complications.

To address this, we propose **DGHME**, which integrates clinical-pathological grouping knowledge into a multi-task learning (MTL) architecture. The model features:
1.  A **Bottom-layer Self-attention Shared Expert** network to filter noise and extract relevant features.
2.  A **Hierarchical Structure** comprising group-internal shared experts, task-private experts, and global shared experts.
3.  An **Adaptive Gating Mechanism** and **Uncertainty-based Loss Weighting** strategy to balance learning across tasks.

Experiments on real-world datasets show that DGHME significantly outperforms state-of-the-art baselines (including MMoE, PLE, and STEM-Net) in both AUC-ROC and AUC-PR metrics.

## 🏗️ Model Architecture

![Model Framework](https://github.com/ohiotxw/MTL/blob/main/图123.pdf)


## 📂 Project Structure

```

DGHME/
├── data/                   \# Data preprocessing scripts and sample data
│   ├── preprocess.py       \# One-hot encoding and standardization
├── models/                 \# Model definitions
│   ├── dghme.py            \# Main DGHME model architecture
│   ├── layers.py           \# Self-attention, Gating networks, Towers
│   └── baselines.py        \# MMoE, Shared-Bottom, etc.
├── utils/                  \# Utility functions
│   ├── metrics.py          \# AUC-ROC, AUC-PR calculation
│   └── loss.py             \# Uncertainty-based loss weighting
├── train.py                \# Main training script
├── config.py               \# Hyperparameter configurations
├── requirements.txt        \# Dependencies
└── README.md

````

## 🛠️ Requirements

The code was tested with **PyTorch**.
Install dependencies via:

```bash
pip install -r requirements.txt
````

**Core Dependencies:**
  * torch
  * numpy
  * pandas
  * scikit-learn
  * matplotlib
    
## 📊 Dataset

The study utilizes a dataset from the **Population Health Data Archive (PHDA)** containing 3,000 T2DM patient records.

  * **Features:** 46 total (8 physiological + 38 biochemical).

> **Note:** Due to privacy regulations, the raw dataset is not included in this repository. Researchers can request access via the China National Center for Population Health Science and Data.

**Data Format Expectations:**

  * Numerical features should be standardized (Zero mean, Unit variance).
  * Categorical features should be One-hot encoded.

## 🚀 Usage

### 1\. Configuration

You can adjust hyperparameters in `config.py`. The default settings used in the paper are:

  * **Batch Size:** 64
  * **Learning Rate:** 0.001
  * **Optimizer:** Adam
  * **Dropout:** 0.4
  * **Epochs:** 500
  * **Bottom Experts:** 4
  * **Hierarchical Experts:** 2 per group, 2 private, 2 global

### 2\. Training

To train the DGHME model:

```bash
python train.py --model DGHME --epochs 500 --batch_size 64
```



