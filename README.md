# 🧠 Optiver - Trading at the Close: Predictive Modeling

A market microstructure modeling project for the **Optiver Trading at the Close** Kaggle competition, developed as part of the **MSBA 6421 - Predictive Analytics** course at the Carlson School of Management.

📌 [Competition Link](https://www.kaggle.com/competitions/optiver-trading-at-the-close/overview)

---

## 📌 Problem Statement

The **closing auction** on NASDAQ plays a critical role in determining the official end-of-day stock prices. It is characterized by:

- A spike in trading volume
- Sudden shifts in buy/sell imbalance
- Increased spreads and price volatility

This project builds a predictive pipeline to model auction **imbalance size** in real-time, helping traders anticipate pressure points in the last 540 seconds before the market closes.

---

## 🎯 Project Objectives

- Segment the final 540 seconds into **three meaningful time windows**
- Engineer microstructure features capturing real-time signals
- Train and validate predictive models tailored to each window
- Blend predictions to produce stock-level imbalance forecasts
- Optimize for **fast inference**, **low MAE**, and **robustness to feature drift**

---

## 🧪 Window-Based Modeling Strategy

| Window | Time Interval (Seconds) | Key Characteristics |
|--------|--------------------------|----------------------|
| Window 1 | 0–290      | Early signals, tight spreads, low volatility |
| Window 2 | 300–470    | Auction book dynamics emerge, imbalance buildup begins |
| Window 3 | 480–540    | Peak imbalance, volatility spike, final match pressure |

Each window was modeled **independently**, with its own features, model type, and hyperparameters.

---

## 🔧 Feature Engineering Overview

We created over **220 features** per record, grouped into:

1. **Calculated Microstructure Features**  
   E.g., `spread`, `wap_diff`, `order_flow_imbalance`

2. **Same-Day Historical**  
   Intraday rolling stats (`sd_mean`, `delta_sd`, `initial_0s`)

3. **Intra-Window Dynamics**  
   Momentum and drift within the same window (`delta_within_window`, `sw_mean`)

4. **Inter-Window Comparison**  
   Signals from previous windows (`Lag_`, `Beg_Window`)

5. **Cross-Day Historical Context**  
   Rolling features over previous days (`rolling_mean_10_`)

---

## 🤖 Models and Performance

| Window | Models Evaluated      | Best MAE     |
|--------|------------------------|--------------|
| 0–290s | CatBoost, GRU          | **6.11 (CatBoost)** |
| 300–470s | CatBoost, GRU         | **5.22 (CatBoost)** |
| 480–540s | CatBoost, GRU, LightGBM | **4.98 (CatBoost)** |

🏁 **Final Blended MAE:** `5.4404`  
Due to Kaggle API issues, the final evaluation was conducted locally using `revealed_targets.csv`.

---

## 🚀 Deployment-Ready Features

- ✅ **Fast Inference:** Tree-based models (CatBoost) with low latency
- ✅ **Pickled Models:** Ready for integration in production
- ✅ **Compact Feature Set:** Efficient memory usage
- ✅ **Modular Pipeline:** Supports per-window predictions

---

## 📁 Project Structure
optiver-trading-at-the-close-predictive-modeling/
├── data/ # Raw and processed input files
├── notebooks/ # EDA and modeling notebooks
├── models/ # Trained model files (.pkl)
├── outputs/ # Submission files, logs, MAE reports
├── utils/ # Custom feature engineering scripts
└── README.md # Project documentation

---

## 👥 Team

- Aurosikha Mohanty  
- Ujjwal Khanna  
- Sahil Sinha  
- Harshal Sable  

---

## 📬 Contact

For questions or collaboration inquiries, feel free to reach out via GitHub or LinkedIn.

---
