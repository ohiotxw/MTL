这是一个为您准备的 GitHub `README.md` 文档草稿。它是根据您提供的论文内容（DGHME模型）编写的，结构符合开源学术代码仓库的标准规范。

您可以直接复制以下 markdown 代码到您的项目中，并根据您实际的代码文件结构稍作调整。

-----

```markdown
# DGHME: A Hierarchical Hybrid Expert Multi-task Learning Model for Disease Grouping

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Framework](https://img.shields.io/badge/PyTorch-1.8%2B-orange.svg)](https://pytorch.org/)

This repository contains the official implementation of the paper: **"DGHME: A Hierarchical Hybrid Expert Multi-task Learning Model for Disease Grouping in Diabetes Complication Prediction"** (IEEE Journal of Biomedical and Health Informatics).

**DGHME** (Disease-Grouping Hierarchical Mixed Expert) is a novel multi-task learning framework designed to predict four major complications of Type 2 Diabetes Mellitus (T2DM): **Diabetic Retinopathy (DR)**, **Diabetic Nephropathy (DN)**, **Coronary Heart Disease (CHD)**, and **Fatty Liver Disease (FLD)**.

## 📖 Abstract

Accurate identification and prediction of diabetes complications are crucial for improving patient health. However, existing prediction models predominantly employ single-task learning (STL) paradigms, failing to fully leverage the intrinsic correlations among different complications.

To address this, we propose **DGHME**, which integrates clinical-pathological grouping knowledge into a multi-task learning (MTL) architecture. The model features:
1.  A **Bottom-layer Self-attention Shared Expert** network to filter noise and extract relevant features.
2.  A **Hierarchical Structure** comprising group-internal shared experts, task-private experts, and global shared experts.
3.  An **Adaptive Gating Mechanism** and **Uncertainty-based Loss Weighting** strategy to balance learning across tasks.

Experiments on real-world datasets show that DGHME significantly outperforms state-of-the-art baselines (including MMoE, PLE, and STEM-Net) in both AUC-ROC and AUC-PR metrics.

## 🏗️ Model Architecture

The DGHME framework is designed based on pathophysiological connections:
* **Microvascular Group:** DR and DN (Shared mechanisms: hyperglycemia, polyol pathway activation).
* **Cardio-Metabolic Group:** CHD and FLD (Shared mechanisms: insulin resistance, dyslipidemia).

![Model Framework](path/to/your/image/Fig3_DGHME_framework.png)
*(Note: Please replace the path above with the actual path to Figure 3 from your paper)*

## 📂 Project Structure

```

DGHME/
├── data/                   \# Data preprocessing scripts and sample data
│   ├── preprocess.py       \# One-hot encoding and standardization
│   └── ...
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

The code was tested with **Python 3.8+** and **PyTorch**.
Install dependencies via:

```bash
pip install -r requirements.txt
````

**Core Dependencies:**

  * torch
  * numpy
  * pandas
  * scikit-learn
  * matplotlib (for plotting results)

## 📊 Dataset

The study utilizes a dataset from the **Population Health Data Archive (PHDA)** containing 3,000 T2DM patient records.

  * **Features:** 46 total (8 physiological + 38 biochemical).
  * **Tasks:** Binary classification for DR, DN, CHD, FLD.

> **Note:** Due to privacy regulations, the raw dataset is not included in this repository. Researchers can request access via the China National Center for Population Health Science and Data or use their own tabular datasets formatted similarly (Rows: Patients, Cols: Features + Labels).

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

To train baseline models (e.g., MMoE, Shared-Bottom):

```bash
python train.py --model MMoE
```

## 📈 Results

DGHME achieves superior performance compared to single-task (GBDT, DNN) and multi-task baselines.

| Model | Avg AUC-ROC | Avg AUC-PR |
| :--- | :---: | :---: |
| GBDT | 0.7673 | 0.6757 |
| DNN | 0.7591 | 0.6692 |
| MMoE | 0.7682 | 0.6818 |
| STEM-Net | 0.7775 | 0.6900 |
| **DGHME (Ours)** | **0.8014** | **0.7141** |

*Results based on 5-fold cross-validation.*

## 🤝 Citation

If you find this work useful for your research, please cite our paper:

```bibtex
@article{tang2024dghme,
  title={DGHME: A Hierarchical Hybrid Expert Multi-task Learning Model for Disease Grouping in Diabetes Complication Prediction},
  author={Tang, Xiaowei and Li, Hongru and Han, Bowen and Wang, Chenglei and Xu, Lisheng and Yu, Xia},
  journal={IEEE Journal of Biomedical and Health Informatics},
  year={2024},
  publisher={IEEE}
}
```

## 📧 Contact

For any questions, please contact:

  * Xiaowei Tang: tangxw@stumail.neu.edu.cn
  * Xia Yu (Corresponding Author): yuxia@ise.neu.edu.cn

## Acknowledgments

This work was supported by the Noncommunicable Chronic Diseases-National Science and Technology Major Project and the National Natural Science Foundation of China.

```

### 说明与建议：

1.  **图片占位符**：我在文档中留了 `![Model Framework](path/to/your/image/Fig3_DGHME_framework.png)`。建议您将论文中的 **Fig. 1 (Overall structure)** 或 **Fig. 3 (DGHME framework)** 截图保存为图片文件（如 png），放入仓库的文件夹中，并替换该路径。这样能大大增加 Readme 的可读性。
2.  **BibTeX 年份**：我在 Citation 中写了 2024，如果论文最终发表年份是 2025，请手动修改。
3.  **代码结构**：`Project Structure` 部分是假设的标准结构。如果您的实际代码结构不同（例如所有代码都在一个文件中），请相应修改该部分。
4.  **License**：如果您打算开源代码，记得在仓库中添加一个 `LICENSE` 文件（如 MIT 或 Apache 2.0），这对于学术代码也是推荐的。
```
