# NGAFID Aviation Predictive Maintenance

![Python](https://img.shields.io/badge/Python-3.10-blue) ![Status](https://img.shields.io/badge/Status-In%20Progress-yellow) ![License](https://img.shields.io/badge/License-MIT-green)

End-to-end predictive maintenance project using the **National General Aviation Flight Information Database (NGAFID)** — the largest publicly available annotated fleet-wide dataset for aviation maintenance research. This project predicts whether a flight occurs **within 2 days before an unplanned maintenance event**, enabling proactive fault detection and reducing unscheduled aircraft downtime.

---

## Dataset

- **Source**: [NGAFID Aviation Maintenance Dataset — Kaggle](https://www.kaggle.com/datasets/hooong/aviation-maintenance-dataset-from-the-ngafid)
- **Size**: 31,177 hours of real general aviation flight data across 28,935 flights
- **Maintenance events**: 2,111 unplanned maintenance events across 36 fault types
- **Structure**:
  - `flight_header.csv` — flight-level index with maintenance labels, `date_diff`, `before_after`, fault hierarchy
  - `flight_data.pkl` — dictionary of 11,446 per-flight NumPy arrays (shape: timesteps x 23 sensor channels)

---

## Project Goals

- Build flight-level features from raw multivariate sensor time-series (23 channels)
- Define a realistic binary classification target: **maintenance within 2 days** (pre-event flights only)
- Train and evaluate baseline ML models (Random Forest / XGBoost)
- Export modeling dataset and predictions for Power BI dashboard visualisation
- Compare against published benchmark models from the original NGAFID research paper

---

## Methodology

### 1. Feature Engineering
Each flight's raw sensor array (shape: `timesteps x 23`) is summarised into statistical features per sensor channel:
- Mean, Standard Deviation, Min, Max per channel
- Results in a flat feature vector of 92 features per flight

### 2. Target Definition
- **Positive (1)**: `before_after == "before"` AND `date_diff >= -2` (flight within 2 days before maintenance)
- **Negative (0)**: All other flights (far from event, post-event, or same-day)

### 3. Modelling
- Baseline: `RandomForestClassifier` with `class_weight="balanced"` to handle class imbalance
- Evaluation metrics: ROC-AUC, Precision, Recall, F1-Score, Confusion Matrix

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python (Google Colab) | Data loading, feature engineering, modelling |
| Pandas / NumPy | Data wrangling and feature computation |
| Scikit-learn | Random Forest baseline and evaluation |
| XGBoost | Advanced gradient boosting baseline |
| Power BI | Dashboard for fault trend and model output visualisation |
| GitHub | Version control and portfolio hosting |

---

## Repository Structure

```
ngafid-aviation-predictive-maintenance/
|-- README.md
|-- LICENSE
|-- .gitignore
|-- notebooks/
|   |-- ngafid_predictive_maintenance.ipynb   # Main Colab notebook
|-- data/
|   |-- flight_header_sample.csv              # Sample label file (full data via Kaggle)
|-- reports/
|   |-- model_predictions.csv                 # Exported predictions for Power BI
```

---

## Results (Baseline)

> To be updated after model training is complete.

---

## Business Impact

- Shifts aircraft maintenance from **reactive to proactive**, reducing unscheduled AOG (Aircraft on Ground) events
- A 2-day advance warning window gives MRO teams actionable lead time to source parts and schedule manpower
- Directly applicable to airline fleet health management and MRO cost optimisation

---

## References

- Yang, H. & Desell, T. (2022). *NGAFID: The National General Aviation Flight Information Database*. AAAI.
- Dataset: https://www.kaggle.com/datasets/hooong/aviation-maintenance-dataset-from-the-ngafid
- Companion code: https://github.com/hyang0129/NGAFIDDATASET

---

## Author

**Kiran Ashok Thomas**  
MSc Aviation Digital Technology & Management — Cranfield University  
[LinkedIn](https://www.linkedin.com/in/kiranashokthomas) | [GitHub](https://github.com/kiranashokthomas)
