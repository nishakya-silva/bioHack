 Dengue Outbreak Prediction System (Sri Lanka)
================================================

An end-to-end **machine learning pipeline** to predict monthly dengue case counts at **district level in Sri Lanka**, using historical dengue surveillance data, weather patterns, geography, and urbanization factors. The model is interpretable, lag-aware, and designed for **early outbreak warning**.

Project Highlights
---------------------

*   **Data sources combined**: Dengue cases (2010–2020) + weather + geography
    
*   **Lag-aware modeling**: Captures delayed biological response (1–3 month lags)
    
*   **Climate-driven features**: Temperature, rainfall, humidity
    
*   **Urbanization factor**: Custom district-level urban score
    
*   **Model**: XGBoost Regressor
    
*   **Explainability**: SHAP-based local explanations
    
*   **Performance**: R² ≈ **0.70**, MAE ≈ **48 cases**
    
*   **Output**: Actionable “clinical-style” outbreak reports with confidence ranges
    

Data Sources
---------------

1.  **Historical Dengue Cases (2010–2020)**
    
    *   District-level monthly case counts
        
2.  **Weather Data**
    
    *   Average temperature
        
    *   Average precipitation
        
    *   Average humidity
        
3.  **Geographic Reference**
    
    *   Latitude, Longitude, Elevation
        
    *   Province
        

Feature Engineering
-----------------------

### Temporal Features

*   Month
    
*   Cases\_Lag1 (previous month cases – momentum feature)
    

### Climate Lags (1–3 months)

*   Precip\_Lag1, Precip\_Lag2, Precip\_Lag3
    
*   Temp\_Lag1, Temp\_Lag2, Temp\_Lag3
    

### Spatial & Socio-Urban Features

*   Latitude, Longitude, Elevation
    
*   Urban\_Score (custom scale 1–10 per district)
    

### Missing Data Strategy

*   **Monthly mean imputation** (climate variables filled by same-month averages)
    

Model Architecture
---------------------

*   **Algorithm**: XGBoost Regressor
    
*   **Key Hyperparameters**:
    
    *   n\_estimators = 500
        
    *   learning\_rate = 0.05
        
    *   max\_depth = 6
        
    *   subsample = 0.8
        

### Train/Test Split

*   Time-aware split (80% train, 20% test)
    
*   No shuffling to preserve temporal order
    

Model Performance
--------------------

MetricValueMean Absolute Error (MAE)~48 casesR² Score~0.70

The model captures **seasonality, outbreak momentum, and climate triggers** effectively.

Explainability (SHAP)
------------------------

*   Uses **TreeExplainer** for XGBoost
    
*   Provides **local explanations** for individual district forecasts
    
*   Identifies which factors:
    
    *   Increased outbreak risk
        
    *   Reduced outbreak risk
        

Example insights:

*   High temperature 1-month lag → strong risk increase
    
*   Previous month cases → outbreak momentum
    
*   Geographic location modifies baseline risk
    

Example Forecast Output
--------------------------

**District**: Kegalle**Predicted Cases (Next Month)**: **187****95% Confidence Range**: **93 – 280 cases**

**Interpretation**:

*   Risk driven primarily by elevated recent temperature
    
*   Momentum from prior month cases
    
*   Overall risk slightly **below national average**, but trending upward
    

Model Export
---------------

The trained model is saved as: final_dengue_model.pkl 

This can be reused for:

*   Future forecasts
    
*   Web dashboards
    
*   Public health early-warning systems
    

Potential Applications
-------------------------

*   Early dengue outbreak alerts
    
*   Hospital resource planning
    
*   Public health decision support
    
*   Climate-health research
    

Future Improvements
----------------------

*   Add mosquito index / entomological data
    
*   Use LSTM or Temporal Fusion Transformers
    
*   Province-specific calibration
    
*   Real-time weather API integration
    
*   Web dashboard (Streamlit / Dash)
    

Authors & Credits
-----------------------

Developed as part of an **AI for Public Health** initiative using Sri Lankan dengue surveillance data.

_Predict early. Act faster. Save lives._
