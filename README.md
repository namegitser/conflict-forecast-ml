# 🌍 Conflict Forecasting & Risk Analysis (Middle East)

## 📌 Overview
This project builds a machine learning system to analyze and forecast conflict intensity in the Middle East using historical data from ACLED (Armed Conflict Location & Event Data Project). The system combines regression and classification to both predict future fatalities and identify high-risk regions where conflict may escalate.

---

## 🎯 Problem Statement
Given historical weekly conflict data, the goal is to predict whether a region will experience a significant increase in conflict (fatalities) in the upcoming week. This enables early warning signals for governments, analysts, and humanitarian organizations to take proactive measures.

---

## 📊 Dataset
The dataset contains weekly aggregated conflict data with the following key features:

- WEEK → Time (weekly)
- REGION → Geographic region
- COUNTRY → Country name
- ADMIN1 → State/Province
- EVENT_TYPE / SUB_EVENT_TYPE → Nature of conflict
- EVENTS → Number of incidents
- FATALITIES → Number of deaths
- POPULATION_EXPOSURE → Exposure metric (partially available)
- CENTROID_LATITUDE / LONGITUDE → Geographic coordinates

### 📌 Data Characteristics
The dataset is highly skewed:
- Most weeks have 0–1 fatalities
- Few weeks contain extreme spikes (100+ or even 1000+)
- This makes prediction challenging and realistic

---

## 🧠 Approach

### 1. Data Preparation
- Converted WEEK to datetime format
- Sorted data by COUNTRY and time
- Handled missing values and ensured temporal consistency

---

### 2. Feature Engineering
We created time-based features to capture temporal patterns:

- Lag features:
  - fatalities_lag1, fatalities_lag2, fatalities_lag3
- Rolling statistics (window = 4 weeks):
  - fatalities_roll_mean
  - fatalities_roll_std
- Event-based features:
  - events_lag1

These features help the model understand recent conflict trends.

---

### 3. Modeling (Hybrid Approach)

#### 🔹 Regression Model
We first predict the number of fatalities in the next week.

- Model: Random Forest Regressor
- Target: next_week_fatalities
- Evaluation Metric: Mean Absolute Error (MAE)

Result:
- MAE ≈ 8.7 fatalities

This means the model is off by ~9 fatalities on average, which is reasonable given the high variability in the data.

---

#### 🔹 Risk Classification Layer
We convert predicted fatalities into actionable risk categories.

Rule:
- If predicted fatalities > 1.5 × recent average → HIGH RISK
- Else → LOW RISK

This transforms raw predictions into decision-friendly outputs.

---

## 📈 Results & Insights
- The model captures general conflict trends over time
- Performs well on normal weeks (low fatalities)
- Struggles with extreme spikes (due to rarity and skewness)
- Rolling averages and lag features are strong predictors

---

## 🗺️ Dashboard (Planned / Implemented)
The project includes (or will include) a Streamlit-based dashboard:

- Interactive map of the Middle East
- Color-coded risk levels:
  - 🔴 High Risk
  - 🟢 Low Risk
- Country-wise trend visualization
- Predicted vs actual comparison

---

## 🛠️ Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib / Plotly
- Streamlit (for dashboard)
- Git & GitHub (with CI/CD pipeline)

---

## 📁 Project Structure
conflict-forecast-ml/
│
├── data/
│ ├── raw/
│ └── processed/
├── notebooks/
│ ├── eda.ipynb
│ └── modeling.ipynb
├── src/
├── app/
├── .github/
├── README.md


---

## 🔮 Future Improvements
- Integrate real-time news or social media signals
- Use advanced models (XGBoost, LSTM)
- Improve spike detection with better thresholds
- Automate data ingestion and pipeline
- Deploy fully real-time monitoring system

---

## 💡 Key Takeaway
This project demonstrates how data engineering, machine learning, and visualization can be combined to build a real-world system for conflict monitoring and forecasting.

