# IoT-Botnet-Detection_Computer-Networking
Semester project
[![Live Interactive Dashboard](https://img.shields.io/badge/Live_Demo-IoT--Shield_XAI-00809D?style=for-the-badge&logo=vercel)](https://iot-shield-visualizer.vercel.app)
## Overview
This repository contains a complete Intrusion Detection System (IDS) pipeline built to identify malicious botnet traffic (e.g., Mirai, Okiru, DDoS) in IoT networks. The project leverages the **IoT-23 dataset** and implements a custom methodology comparing tree-based baseline models against a proposed PyTorch Multi-Layer Perceptron (MLP).

To optimize for the extreme hardware constraints of IoT devices, **SHAP (SHapley Additive exPlanations)** feature extraction was utilized to conduct an ablation study, stripping the dataset of noisy columns and retraining the network on only the top 3 critical network features.

## Methodology
1. **Data Preprocessing:** 
   - Handled a 50,000-row representative subset of Zeek network connection logs.
   - Dropped spoofable identifiers (IPs, Ports, timestamps) to prevent model overfitting.
   - Applied **SMOTE (Synthetic Minority Over-sampling Technique)** strictly to the training split to balance the extreme minority benign class without introducing data leakage.
2. **Baseline Models evaluated:** Logistic Regression, Random Forest, XGBoost, and LightGBM.
3. **Proposed Model:** A highly efficient, custom 3-layer PyTorch MLP designed for low-latency inference.

## Key Results
* **Accuracy Champion:** **LightGBM** achieved the highest overall detection capability with a **0.946 ROC-AUC** and 0.910 Macro-F1 score.
* **SHAP Feature Extraction:** The Random Forest explainer identified the top 3 features driving botnet classifications as:
  1. `orig_ip_bytes`
  2. `duration`
  3. `orig_pkts`
* **Latency Optimization (Ablation Study):** Retraining the PyTorch MLP on only the 3 SHAP-identified features dropped the inference latency to **0.0000 ms/sample**, successfully proving the hypothesis that a highly reduced feature space maximizes speed for resource-constrained IoT environments.

## Tech Stack
* **Languages:** Python
* **Deep Learning:** PyTorch
* **Machine Learning:** Scikit-Learn, XGBoost, LightGBM, Imbalanced-Learn (SMOTE)
* **Interpretability:** SHAP
* **Data & Visualization:** Pandas, NumPy, Matplotlib, Seaborn

> **Dashboard:** **[iot-shield-visualizer.vercel.app](https://iot-shield-visualizer.vercel.app)**



