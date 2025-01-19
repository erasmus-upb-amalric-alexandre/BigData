# Forecasting Transaction Volumes on the XRP Ledger Using Machine Learning

**Author**: Alexandre Amalric  
**Affiliation**: XRPL Commons - Ripple  
**Date**: January 2025  

---

## **Abstract**
This project extends the work done in the 13 Stock Predictor Big Data project and transitions to the more complex task of forecasting transaction volumes on the XRP Ledger. The focus is on leveraging advanced time-series forecasting models like RNNs, GRUs, LSTMs, and Transformers to predict transaction trends using historical and auxiliary data. By addressing challenges like high volatility, complex temporal dependencies, and data heterogeneity, the study aims to deliver actionable insights for blockchain validators, investors, and developers within the XRPL ecosystem.

---

## **Table of Contents**
1. [Introduction](#introduction)
2. [Data Preparation](#data-preparation)
3. [Model Selection](#model-selection)
4. [Experiment Setup](#experiment-setup)
5. [Results and Analysis](#results-and-analysis)
6. [Conclusion and Future Work](#conclusion-and-future-work)

---

## **Introduction**

### **Background**
The XRP Ledger (XRPL) is a high-performance blockchain optimized for fast and low-cost cross-border payments. Forecasting transaction volumes on XRPL has significant implications for:
- Operational efficiency.
- Risk management.
- Investment strategies.

### **Objective**
This project develops a machine learning framework to predict transaction volumes using time-series forecasting techniques, combining on-chain and off-chain data.

### **Challenges**
- High volatility in transaction volumes.
- Complex temporal dependencies (e.g., seasonal or weekly trends).
- Anomalies like sudden spikes or dips due to market events.
- Scalability for processing large datasets from the XRPL.

---

## **Data Preparation**

### **Data Sources**
1. **XRPL Datasets**:
   - `ledger.db` (40 GB): Includes ledger sequence numbers, closing times, and total coins in circulation.
   - `transaction.db` (8.2 TB): Contains transaction-level details like types and amounts.

2. **External Data**:
   - Market indicators (e.g., XRP price, trading volume) from CoinGecko.
   - Social media sentiment data from Twitter and Reddit.
   - Global economic indicators like inflation and interest rates.

### **Feature Engineering**
- Lagged features: Capturing autocorrelation in transaction volumes.
- Time-based features: Day of the week, month, and hour to capture cyclic patterns.
- Encoded transaction types: Differentiating between payments, trustlines, and smart contracts.

### **Data Preprocessing**
- **Normalization**: Scaling values between 0 and 1 using Min-Max scaling.
- **Handling Missing Values**: Using forward filling to interpolate gaps in the dataset.

---

## **Model Selection**

### **Roadmap**
1. **Baseline Models**:
   - Simple RNN: Captures short-term dependencies.
2. **Intermediate Models**:
   - GRU: Handles medium-term dependencies with gating mechanisms.
   - LSTM: Captures long-term dependencies using memory cells.
3. **Advanced Models**:
   - Temporal Convolutional Networks (TCNs): Avoid vanishing gradient issues and process longer sequences efficiently.
   - Transformer-based models (e.g., Temporal Fusion Transformer): Use self-attention to capture dependencies across long horizons.

### **Evaluation Metrics**
- **MAE**: Mean Absolute Error.
- **RMSE**: Root Mean Squared Error.
- **sMAPE**: Symmetric Mean Absolute Percentage Error.
- **\( R^2 \)**: Coefficient of Determination.

---

## **Experiment Setup**

### **Data Splitting**
- 80% training and 20% testing to evaluate model generalization.

### **Hyperparameter Tuning**
- Learning rate: 0.001
- Batch size: 64
- Epochs: 100

---

## **Results and Analysis**

### **Model Performance**
| Model         | RMSE    | MAE     | sMAPE   | \( R^2 \)  |
|---------------|---------|---------|---------|------------|
| XGBoost       | 0.3108  | 0.2938  | 89.31%  | -11.02     |
| Random Forest | 0.1801  | 0.1652  | 63.74%  | -3.04      |
| DeepAR        | 0.0990  | 0.0630  | 32.68%  | -0.22      |
| LSTM          | 0.0995  | 0.0740  | 35.36%  | -0.23      |

### **Key Insights**
- **DeepAR** performed the best in terms of RMSE and MAE but failed to align with actual trends (\( R^2 < 0 \)).
- Tree-based models like XGBoost and Random Forest struggled due to their inability to capture temporal dependencies.

---

## **Conclusion and Future Work**

### **Summary of Findings**
- DeepAR and LSTMs showed better performance than tree-based models.
- Challenges like high volatility and anomalies in transaction volume trends remain significant.

### **Future Directions**
1. Explore hybrid models (e.g., CNN-Transformer).
2. Integrate additional external data sources.
3. Refine preprocessing techniques to handle seasonal components effectively.

---
