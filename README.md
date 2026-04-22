# Multi-Station Streamflow Prediction using LSTM

##  Google Colab Links

*  **Model Training Notebook:** [Add Your Colab Link Here]
*  **EDA & Data Analysis Notebook:** [Add Your Colab Link Here]

---

#  Project Overview

This project focuses on predicting **daily streamflow** using a **Long Short-Term Memory (LSTM)** deep learning model across **multiple hydrological stations**.

Instead of training separate models for each station, a **global LSTM model** is developed that:

* Learns **shared hydrological patterns**
* Retains **station-specific characteristics** using embeddings

---

# ` Dataset Description

##  Data Source

* CAMELS India dataset (streamflow observations)
* Time period: **1980 – 2020 (~41 years)**

##  Data Format

The dataset is structured as:

| year | month | day | Station_1 | Station_2 | ... |
| ---- | ----- | --- | --------- | --------- | --- |
| 1980 | 1     | 1   | value     | value     | ... |

### Key Points:

* Each **column (after date)** represents a station
* Each **row** represents daily streamflow values
* Units: typically **m³/s (cubic meters per second)**

---

#  Exploratory Data Analysis (EDA)

The EDA notebook includes:

* Missing value handling (interpolation)
* Station-wise statistics
* Time-series visualization
* Distribution analysis
* Trend and seasonality inspection

### Purpose of EDA:

* Understand variability in streamflow
* Identify anomalies and missing data
* Prepare clean input for model training

---

#  Data Preprocessing

### Steps:

1. **Date Conversion**

   * Combine year, month, day → datetime index

2. **Missing Value Handling**

   * Linear interpolation

3. **Station Filtering**

   * Remove stations with insufficient data

4. **Normalization**

   * Min-Max scaling applied **independently per station**

5. **Sequence Creation**

   * Input: past **30 days**
   * Output: next day streamflow

---

#  Model Architecture

The model uses a **multi-input LSTM architecture**:

###  Inputs:

1. **Time Series Input**

   * Shape: (30 days, 1 feature)

2. **Station ID Input**

   * Encoded using **Embedding layer**

---

##  Model Components:

* LSTM Layer (64 units)
* LSTM Layer (32 units)
* Embedding Layer (station identity)
* Concatenation Layer
* Dense Output Layer

---

#  Model Training Strategy

### Key Idea:

A **single global model** is trained on all stations.

### Why this works:

* Learns **common hydrological behavior**
* Uses **embedding** to distinguish stations
* Improves generalization

---

#  Training Details

* Train-Test Split: **80% – 20%**
* Loss Function: **Mean Squared Error (MSE)**
* Optimizer: **Adam**
* Callbacks:

  * Early Stopping
  * Learning Rate Reduction

---

#  Evaluation Metrics

* RMSE (Root Mean Squared Error)
* MAE (Mean Absolute Error)
* R² Score

Evaluation is done **per station**.

---

#  Future Prediction

The model supports **autoregressive forecasting**:

* Uses last 30 days
* Predicts future values step-by-step

---

#  Workflow (Flowchart)

```
                Raw Data (CSV)
                       │
                       ▼
              Date Processing
                       │
                       ▼
            Missing Value Handling
                       │
                       ▼
             Station-wise Scaling
                       │
                       ▼
             Sequence Generation
                       │
                       ▼
        Combine All Stations Data
                       │
                       ▼
        ┌─────────────────────────┐
        │   LSTM Model Training   │
        │  + Station Embedding    │
        └─────────────────────────┘
                       │
                       ▼
                Model Evaluation
                       │
                       ▼
             Future Prediction
```

---

#  Important Insights

* Each station is **scaled independently**
* Station identity is preserved using **embedding**
* Model learns:

  * Global patterns 
  * Local station behavior 

---



