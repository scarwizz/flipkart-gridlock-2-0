# 🚦 Flipkart Gridlock 2.0: AI-Driven Traffic Intelligence

**Team:** wizzx2.O | **Final Optimized Build**

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?style=for-the-badge&logo=kaggle)](https://www.kaggle.com/code/arpitsingh5134/notebook183cb0238d) 
[![Python](https://img.shields.io/badge/Python-3.10-green?style=for-the-badge&logo=python)]() 
[![Optuna](https://img.shields.io/badge/Optuna-Optimized-red?style=for-the-badge)]()

## 📌 Executive Summary
Traffic congestion in rapidly growing metropolises like Bengaluru is a fluid, highly volatile physics problem. Traditionally, predicting gridlock requires heavy reliance on external, real-time APIs (Google Maps, TomTom). 

Operating under the strict constraint of **No External Data**, this pipeline constructs robust internal proxies for congestion using purely historical parking violation data. We successfully decoupled "where police patrol" from "where traffic happens" to build a proactive, bias-aware traffic intelligence system for the Bengaluru Traffic Police (BTP).

---

## 🏗️ Core Architectures

Our pipeline is split into two specialized engines, driven by aggressive hyperparameter optimization and dynamic validation windows:

### 1. System 1: Routine Hotspot Management (Optuna-Tuned Hybrid Ensemble)
* **Objective:** Predict continuous congestion severity for stable, recurring hotspots.
* **The Science (Residual Learning):** Tree models struggle to extrapolate averages but excel at non-linear variance. We mathematically split the problem: a historical statistical mean captures the "routine" flow, while an XGBoost + HistBoost ensemble predicts the residual spikes.
* **Defeating Concept Drift:** By implementing a strict **8-week sliding window** validation, we forced the model to "forget" stale historical data, aligning predictions with current urban mobility trends.

### 2. System 2: Emerging Hotspot Early Warning (Dynamic Focal Loss)
* **Objective:** Predict sudden, catastrophic gridlock anomalies *before* they structurally form.
* **The Science (Rare Event Hunting):** Emerging hotspots are rare (only 6.4% of the data). Standard classifiers fail here. We implemented a custom **Focal Loss objective** in LightGBM to handle extreme class imbalance.
* **The Bayesian Sniper:** Using Optuna, we mathematically tuned the focal error gradients ($\gamma=1.288$, $\alpha=0.356$) to aggressively hunt anomalies without drowning in false positives.

---

## 📊 Key Performance Indicators (KPIs)

| Metric | Result | Operational Significance |
| :--- | :--- | :--- |
| **Precision@10 (System 1)** | `0.600` | Successfully broke the hardened 0.593 baseline. Highly accurate daily beat planning. |
| **Anomaly Recall (System 2)** | `47%` | Catches nearly half of all sudden gridlock anomalies *before* they form. |
| **System 2 F1-Score** | `0.32` | 3x improvement in overall sensitivity compared to standard cross-entropy models. |

---

## 🧠 Explainable AI (XAI) & Fairness

For law enforcement to trust an AI, it cannot operate in a black box.

* **SHAP Decision Mapping:** Explainable AI reveals that our engineered "Physics of Flow" features—specifically **Spatial Spillover** (`delta_neighbor_count` using a 500m KDTree) and **Commercial Surges** (`heavy_weekend_risk`)—are the absolute top drivers for predicting gridlock.
* **Algorithmic Fairness (Bias Check):** We ran a spatial distribution check across police administrative zones (`center_code`). It yielded a near-zero variance of **0.0011**. This mathematically proves our system identifies true gridlock physics rather than simply reflecting historical patrol bias.

---

## 🚀 Operational Deployment Roadmap

We envision a 4-stage integration with the Bengaluru Traffic Police Command Center:
1. **Ingestion:** Connect daily BTP violation databases directly to the automated cleaning script.
2. **Routine Rosters:** Generate optimized daily patrol schedules using System 1 Hybrid ranking predictions.
3. **Pre-Emptive Dispatch:** Activate control room alerts when System 2 anomaly probabilities spike.
4. **Interventions:** Conduct physical urban audits (e.g., bollards, tow zones) in continuously flagged anomaly zones.

---

## 📁 Repository Structure & Usage

* `phase2-flipkart-gridlock2-o.ipynb`: The core, self-contained end-to-end pipeline.
* `README.md`: Project overview and architectural documentation.

### How to Run
The analysis is entirely self-contained. The raw and processed datasets used in this project are hosted privately on Kaggle. You can run the code and interact with the visualizations directly via the Kaggle environment.

> 👉 **[Run the Full Pipeline on Kaggle](https://www.kaggle.com/code/arpitsingh5134/notebook183cb0238d)**
