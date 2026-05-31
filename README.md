# 🌞 Solar Energy Forecasting — Saudi Arabia

A comprehensive time series forecasting project that predicts **Global Horizontal Irradiance (GHI)** across Saudi Arabia using statistical, machine learning, and deep learning models.

---

## 📌 Project Overview

Saudi Arabia receives some of the highest solar irradiance in the world, making accurate solar energy forecasting critical for grid management and renewable energy planning. This project builds and compares **9 forecasting models** across three model families to identify the most accurate approach for monthly GHI prediction.

**Dataset:** Monthly solar and weather measurements from monitoring stations across all Saudi regions (2017–2021), aggregated into a national average time series of 60 data points.

---

## 🗂️ Project Structure

```
├── TS_project_talal_Fahad.ipynb   # Main notebook
└── README.md
```

---

## 🔄 Workflow

1. **Time Series Exploration** — Visualizing trends, distributions, and seasonality
2. **Stationarity Testing** — ADF test on the original and differenced series
3. **Time Series Decomposition** — Separating trend, seasonality, and residuals
4. **Missing Date Imputation** — Linear interpolation across a complete 60-month range
5. **Feature Engineering** — Lag features (up to 12 months), rolling mean/std windows
6. **Train / Test Split** — Temporal split (no random shuffling) to simulate real forecasting
7. **Model Building** — 9 models across 3 families
8. **Comparison & Selection** — Ranked by RMSE and MAE

---

## 🤖 Models Used

### Statistical
| Model | Description |
|-------|-------------|
| ARMA | Applied on first-differenced series |
| ARIMA | Handles non-seasonal trends |
| SARIMA | Handles both trend and seasonality |

### Machine Learning
| Model | Key Hyperparameters |
|-------|---------------------|
| Linear Regression | Baseline ML model |
| Decision Tree | `max_depth=5` |
| Random Forest | `n_estimators=300`, `max_depth=8` |
| Gradient Boosting | `n_estimators=300`, `learning_rate=0.05` |
| XGBoost | `n_estimators=300`, `subsample=0.8` |

### Deep Learning
| Model | Architecture |
|-------|-------------|
| Simple RNN | 50 units, Dropout 0.2 |
| LSTM | 64 units, Dropout 0.2 |
| GRU | 64 units, Dropout 0.2 |

All deep learning models use:
- Input window: 12 months
- Optimizer: Adam
- Loss: MSE
- Early stopping: patience=10

---

## 📊 Evaluation Metrics

- **RMSE** (Root Mean Squared Error) — primary selection criterion
- **MAE** (Mean Absolute Error)
- **AIC** — for statistical model selection only
---

### 🏆 Model Performance Summary


## 🚀 Getting Started

This notebook was developed in **Google Colab**. To run it:

1. Upload `full_solar_dataset.csv` to your Google Drive or Colab session
2. Update the dataset path in the first code cell:
   ```python
   df = pd.read_csv('/content/full_solar_dataset.csv')
   ```
3. Run all cells in order

### Requirements

```
pandas
numpy
matplotlib
scikit-learn
statsmodels
xgboost
tensorflow
```

Install via:
```bash
pip install pandas numpy matplotlib scikit-learn statsmodels xgboost tensorflow
```

---

## 👥 Authors

**Talal & Fahad** — Data Science Project
