# Flipkart Gridlock 2.0: AI-Driven Traffic Intelligence

This repository contains the prototype pipeline for predictive traffic management in Bengaluru. We operate under the **No External Data** constraint, utilizing only historical parking violation logs to engineer predictive congestion proxies.

## Key Architectures
1. **Hybrid Residual Learning:** Fuses a statistical historical mean with a LightGBM regressor to predict sudden traffic spikes.
2. **Emerging Hotspot Early Warning:** Uses a custom **Focal Loss** objective in LightGBM to handle extreme class imbalance (6.4% frequency) and provide pre-emptive alerts.

## Project Structure
- `/notebooks`: Contains the `Sub_flipkart.ipynb` notebook (your core pipeline).
- `/data`: Contains pre-processed modeling datasets.
- `/results`: Contains SHAP importance plots and experimental metrics.
## Data
The raw and processed datasets used in this project are hosted on Kaggle:
[Access the Dataset on Kaggle](https://www.kaggle.com/datasets/arpitsingh5134/flipkart-gridlock2-2-o)

## How to Run
The analysis is self-contained within `Sub_flipkart.ipynb`. You can interact with the results directly on Kaggle:
[[Link to Kaggle Notebook](https://www.kaggle.com/code/arpitsingh5134/phase2-flipkart-gridlock2-o/edit)]

## Operational Results
- **Routine Management:** +0.020 lift in Precision@10 over baseline.
- **Emerging Hotspots:** 3x improvement in recall using Focal Loss.
