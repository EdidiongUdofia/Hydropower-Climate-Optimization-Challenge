# Hydropower Climate Optimization Challenge

This repository presents a complete solution to the **IBM SkillsBuild Hydropower Climate Optimization Challenge**, which aims to forecast daily energy consumption (in kWh) for various consumer devices in Kalam, Pakistan. 

The approach combines advanced data preprocessing, feature engineering, temporal segmentation, and ensemble machine learning to tackle the region’s complex seasonal trends and extreme weather variability.

---

## 🔍 Overview and Objectives

### Goals:
- Predict **daily energy consumption** for consumer devices.
- Capture **seasonal and weather-related usage patterns**.
- Handle **offline periods** and **missing data** effectively.
- Build a **robust model** that generalizes well across devices and time.

---

## ⚙️ ETL Process

### 🟦 Extract
**Data Sources:**
- **Primary dataset:** 5-minute interval consumer energy consumption.
- **Climate data:** Includes temperature, precipitation, wind components, and snowfall.
- **Sample submission:** Defines the prediction format and test set structure.

**Data Formats:**
- Energy data in **CSV**.
- Climate data in **Excel**.

**Considerations:**
- Devices and users not present in the test set were excluded to ensure consistency.

---

### 🟨 Transform

#### 1. Data Cleaning:
- Converted timestamps to datetime format.
- Filtered out devices and users not in the test set.

#### 2. Aggregation:
- Aggregated 5-minute readings into **daily metrics**.
- Computed **mean, std, min, max** for voltage, current, and power factor.

#### 3. Online/Offline Classification:
- Identified weeks with **zero consumption**.
- Classified days as **online** or **offline** to enhance signal quality.

#### 4. Feature Engineering:
- Extracted device and user IDs.
- Added **temporal and cyclical features** (e.g., day of week, month).
- Merged climate features with energy data.
- Integrated **holiday/Ramadan indicators**.
- Engineered **advanced temperature features** (e.g., volatility, extremes, acceleration).

---

### 🟩 Load
Processed intermediate datasets saved as CSV files:
- `offline_days_enriched.csv`: Entire weeks with zero consumption.
- `filtered_online_days_enriched.csv`: Cleaned dataset with only valid "online" records.

---

## 📊 Data Modeling

### Strategic Data Segmentation
The dataset was split into four parts based on temporal patterns:

1. **Data1:** August–September 2024 + October 2023 (late summer/early fall)
2. **Data2:** November–December 2023 + July 2024 (winter and mid-summer)
3. **Data3:** Remaining months with distinct patterns
4. **Data4:** Full dataset (global modeling)

---

### Model Configurations

For each segment, **7 LightGBM models** were trained using distinct configurations:

1. **Precise:** Deep trees, low learning rate  
2. **Feature Selective:** Aggressive feature filtering  
3. **Robust:** Outlier-resilient  
4. **Deep Forest:** Very deep trees, many estimators  
5. **Highly Regularized:** Strong regularization to prevent overfitting  
6. **Fast Learner:** High learning rate for quick training  
7. **Balanced:** Tuned for bias-variance tradeoff  

---

## 🧠 Optimization & Evaluation

- **Cross-Validation:** 5-fold CV used for each model.
- **Bayesian Optimization:** Used to determine optimal ensemble weights.
- **Feature Importance:** Analyzed to understand key drivers of consumption.
- **Performance Metrics:** RMSE tracked for individual models and the final ensemble.

---

## 📁 Final Output

The final solution generates accurate, device-level daily energy forecasts using a robust ensemble of models and deep feature integration—well-suited for real-world climate-aware energy forecasting in remote and seasonally dynamic regions like Kalam.

## Author
Edidiong Udofia
