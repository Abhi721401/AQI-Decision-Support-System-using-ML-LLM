# AQI-Decision-Support-System-using-ML-LLM

An end-to-end explainable machine learning + LLM-based reporting system for analyzing air pollution, identifying its root causes, and generating public-friendly health advisories.
This project combines statistical analysis, machine learning explainability (SHAP), and LLM-based natural language generation (Gemini) to move beyond raw AQI numbers and deliver actionable environmental insights.

# Project Motivation
Air Quality Index (AQI) values are widely reported, but:
They are difficult for the general public to interpret
They do not clearly explain why pollution is high
They lack actionable, personalized health guidance

This project addresses those gaps by:

Analyzing pollution drivers statistically
Quantifying pollution severity using a custom index
Explaining pollution sources using interpretable ML
Automatically generating public health reports using an LLM
Then Evaluates the LLM report if it is accurate , such as fairness , clarity , Actionability

# 📊 Dataset Overview ( Collected from Central Pollution Control Board)
Rows: 10,000
Cities: Major Indian metropolitan cities
Time Span: 2019–2024 (synthetic but realistic)

Key Features

Air pollutants: PM2.5, PM10, NO₂, CO, SO₂, O₃
Meteorological variables: Temperature, Humidity, Wind Speed, Rainfall, Pressure
Human activity indicators: Vehicle Count, Industrial Activity Index
Health metric: Health Impact Score
Target variable: AQI

# Exploratory Data Analysis & Statistics
✔ Analyses Performed
AQI and pollutant distributions
City-wise AQI comparison (min / mean / max)
Correlation analysis (pollutants, traffic, weather)
Hypothesis testing:
Traffic vs Pollution (Pearson correlation)
ANOVA across AQI categories
Principal Component Analysis (PCA)

🔍 Key Findings

No single pollutant or factor linearly dominates AQI
Traffic count alone does not explain pollution spikes
Pollution is multi-factorial and non-linear
PCA shows no dominant component → motivates explainable ML

# Pollution Severity Index (PSI)
To quantify pollution more meaningfully, a custom Pollution Severity Index (PSI) was constructed:

PSI = 0.40 × PM2.5
    + 0.25 × PM10
    + 0.15 × NO₂
    + 0.10 × CO
    + 0.05 × SO₂
    + 0.05 × O₃
This index reflects the relative health impact of pollutants rather than treating them equally.

# Machine Learning Model

Model: Random Forest Regressor
Target: Pollution Severity Index (PSI)
Features: Pollutants + meteorological + traffic variables
Why Random Forest?
Handles non-linearity
Robust to noise
Compatible with SHAP explainability

# Explainability with SHAP

SHAP (SHapley Additive exPlanations) is used to:
Identify dominant pollution drivers
Attribute pollution severity at the feature level

📈 SHAP Insights

PM2.5 and PM10 are the strongest contributors
Traffic-related gases and weather act as secondary modifiers
Confirms scientific understanding of urban air pollution

# Rule-Based Cause Identification

A deterministic reasoning layer identifies real-world causes such as:
Construction and road dust
Heavy traffic congestion
Industrial emissions
Low wind speed (pollution trapping)
Photochemical smog under high temperature

This improves interpretability and trust.

# Health Risk Interpretation

Converts PM2.5 exposure into a “cigarette equivalent”
Classifies AQI into standard health categories
Generates personalized precautions, such as:
                                          Avoid outdoor exercise
                                          Wear N95 masks
                                          Use indoor air purifiers , etc


# LLM-Powered Public Health Reports (Gemini)

The system uses Google Gemini to automatically generate:
Clear, non-technical air quality reports
City-specific explanations
Health risks and immediate actions
⚠️ The LLM is used only for explanation, not prediction.

# 🧠 LLM Output Accuracy & Self-Evaluation (Quality Control)

Large Language Models can generate fluent text, but verifying correctness and usefulness is critical, especially for public health communication.
To address this, the project includes a self-evaluation module, where the LLM (Gemini) critiques its own generated report using a structured evaluation rubric.
This acts as an automated quality assurance layer for:
Factual accuracy
Public clarity
Actionability of health advice

# 🔍 Self-Evaluation Methodology
After generating an air quality report, the system performs a second LLM pass using a dedicated evaluation prompt.
Evaluation Criteria
The report is assessed on:
Factual Correctness
Clarity for the General Public
Actionability of Advice
The LLM produces:
A short qualitative critique
Strengths and weaknesses
A numerical score (out of 10)

# 🛠 Tech Stack

Python
Pandas, NumPy
Matplotlib, Seaborn
Scikit-learn
SHAP
SciPy
Google Gemini API

# 📌 Key Takeaway

Air pollution is not driven by a single factor.
This project demonstrates how statistics + explainable ML + LLMs can be combined to turn complex environmental data into clear, actionable public health intelligence.

### 🧪 Example: Air Quality Report Generation

# 📥 Input (User-Provided Environmental Data)

user_input = {
    "City": "Kolkata",
    "AQI": 312,
    "PM2.5": 186,
    "PM10": 270,
    "NO2": 68,
    "CO": 1.5,
    "SO2": 5.2,
    "O3": 15.7,
    "Temperature (°C)": 12,
    "Humidity (%)": 93,
    "Wind Speed (km/h)": 8,
    "Rainfall (mm)": 0.0,
    "Pressure (hPa)": 1018,
    "Vehicle Count": 340000
}


# 📤 Output (Auto-Generated Public Health Report)

URGENT Air Quality Alert for Kolkata

Air Quality Index (AQI): 312 (Very Poor)

Why the air quality is dangerous:
The current AQI level indicates extremely polluted air that poses serious health
risks to all residents. Fine particulate matter (PM2.5 and PM10) dominates the
pollution profile, allowing toxic particles to penetrate deep into the lungs and
enter the bloodstream.

What is causing the pollution:
• High concentrations of PM2.5 and PM10 from road dust, construction activity,
  and vehicle emissions
• Elevated nitrogen dioxide levels linked to heavy traffic congestion
• Limited wind movement, causing pollutants to remain trapped near ground level

Health risks:
Breathing the current air is equivalent to smoking approximately 8–9 cigarettes
per day. Children, elderly individuals, and people with heart or lung conditions
are at especially high risk of severe respiratory and cardiovascular effects.

Immediate precautions:
• Avoid outdoor exercise and prolonged exposure
• Wear a properly fitted N95 mask when outdoors
• Keep windows closed and use air purifiers indoors
• Seek medical attention if breathing discomfort occurs

# 🔍 Accuracy & Quality Evaluation (LLM Self-Review)

📊 Accuracy Evaluation Output

Overall Assessment:
This air quality public health report is exceptionally well-structured, urgent,
and highly effective for the general public facing an immediate health threat.

Short Critique:
The report successfully converts complex air quality metrics (AQI 312, PM2.5)
into clear and relatable health risks. The "cigarette equivalent" metric is
particularly effective for communicating exposure severity.

Strengths:
• Urgency: The tone appropriately conveys the seriousness of the situation.
• Clarity: Causes, risks, and precautions are logically organized and easy to follow.
• Actionability: Advice is specific, prioritized, and immediately applicable.
• Diagnosis: Correctly identifies dominant pollution sources such as construction
  dust and vehicle-related emissions.

Minor Limitations:
• The AQI label "Very Poor" is technically correct but slightly less severe than
  international labels such as "Hazardous" for AQI > 300.
• Institutional response measures are not discussed, though this is secondary
  for immediate public guidance.

Evaluation Scores:
• Factual Correctness: 5 / 5
• Clarity for General Public: 5 / 5
• Actionability of Advice: 5 / 5

Overall Score:
9.5 / 10
