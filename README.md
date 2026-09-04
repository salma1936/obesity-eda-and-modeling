# Obesity Level Analysis & Prediction

A full-cycle data analytics project that cleans, explores, visualizes, and models a lifestyle/demographic dataset to classify individuals into **7 obesity levels** — from *Insufficient Weight* to *Obesity Type III*. The project combines Python (EDA + Machine Learning), an interactive **Power BI dashboard**, and an AI-generated business insights report.

## 📌 Project Overview

Obesity is driven by a mix of genetics, diet, and lifestyle habits. This project analyzes survey data on eating habits, physical activity, and demographics for individuals from **Mexico, Peru, and Colombia** to:

- Understand what factors are most associated with obesity level
- Build and compare machine learning models that predict obesity classification
- Present findings through an interactive BI dashboard and a stakeholder-facing report

## 📂 Repository Structure

```
Dhub final project/
├── obesity_data (1).csv                      # Raw dataset (2,111 records)
├── obesity_visualize_clean.ipynb             # Data cleaning + EDA notebook
├── obesity_Visualization_dataClean.csv       # Cleaned dataset (output of the EDA notebook)
├── Obesity_Prediction_Modeling_.ipynb        # Feature engineering + ML modeling notebook
├── Obesity Dashboard.pbix                    # Interactive Power BI dashboard
└── AI_Insights_and_Recommendations_Report.pdf # AI-generated insights & business recommendations
```

## 🗂️ Dataset

- **Records:** 2,111 (raw) → 2,090 after cleaning
- **Source population:** Individuals from Mexico, Peru, and Colombia
- **Target variable:** `NObeyesdad` — 7 classes (`Insufficient_Weight`, `Normal_Weight`, `Overweight_Level_I`, `Overweight_Level_II`, `Obesity_Type_I`, `Obesity_Type_II`, `Obesity_Type_III`)

| Feature | Description |
|---|---|
| `Gender`, `Age`, `Height`, `Weight` | Demographics & anthropometrics |
| `family_history_with_overweight` | Family history of being overweight |
| `FAVC` | Frequent consumption of high-caloric food |
| `FCVC` | Frequency of vegetable consumption |
| `NCP` | Number of main meals per day |
| `CAEC` | Eating between meals |
| `SMOKE` | Smoking habit |
| `CH2O` | Daily water intake |
| `SCC` | Calorie consumption monitoring |
| `FAF` | Physical activity frequency |
| `TUE` | Time using technology devices |
| `CALC` | Alcohol consumption frequency |
| `MTRANS` | Mode of transportation |

## ✨ Features & Workflow

### 1. Data Cleaning & EDA — `obesity_visualize_clean.ipynb`
- Data quality assessment: missing-value detection (`FCVC` ~16%, `CALC` ~10%) and duplicate checks
- Cleaning strategy: mean imputation for the numeric `FCVC` field, mode imputation for the categorical `CALC` field, duplicate removal
- Full exploratory analysis: target-class balance, numerical feature distributions (histograms + KDE), categorical feature distributions, boxplot-based outlier detection, and a correlation heatmap
- Bivariate analysis of obesity level against weight, height, physical activity, gender, and family history
- Key discovered patterns:
  - Weight is the dominant driver separating the seven obesity classes
  - Family history of overweight is strongly associated with higher obesity levels (~82% of the sample overall, rising sharply among obese classes)
  - A striking gender split appears at the extremes: Obesity Type II skews almost entirely male, while Obesity Type III skews almost entirely female
- Exports a modeling-ready cleaned dataset (`obesity_Visualization_dataClean.csv`)

### 2. Predictive Modeling — `Obesity_Prediction_Modeling_.ipynb`
- Outlier treatment using an extreme (3×IQR) winsorization rule, capping only genuinely extreme values instead of dropping rows
- Feature engineering: derived `BMI` feature, label encoding for binary fields, ordinal encoding for `CAEC`/`CALC`, one-hot/scaling for the remaining categorical and numeric features
- Trains and compares four classification algorithms on a stratified 80/20 train-test split:

| Model | Test Accuracy |
|---|---|
| Random Forest | **99.8%** |
| Decision Tree | 97.4% |
| SVM (RBF kernel) | 94.3% |
| Logistic Regression | 91.9% |

- Confusion matrices and per-class precision/recall/F1 for every model
- Random Forest feature-importance ranking to identify the strongest predictors
- Exports summary tables (`model_accuracy_summary.csv`, `feature_importance_summary.csv`) for use in the dashboard/report

### 3. Interactive Dashboard — `Obesity Dashboard.pbix`
A Power BI dashboard built on the cleaned dataset for interactive, filterable exploration of obesity distribution, demographics, and lifestyle drivers.

### 4. AI Insights Report — `AI_Insights_and_Recommendations_Report.pdf`
A stakeholder-facing summary that translates the modeling results into business-oriented insights and actionable recommendations, including the top contributing features behind obesity risk.

## 🛠️ Tech Stack

- **Language:** Python 3
- **Libraries:** pandas, NumPy, Matplotlib, Seaborn, scikit-learn (Logistic Regression, Decision Tree, Random Forest, SVM)
- **BI Tool:** Power BI
- **Environment:** Jupyter / Google Colab notebooks

## 🚀 Getting Started

1. Clone the repository
   ```bash
   git clone <your-repo-url>
   cd "Dhub final project"
   ```
2. Install dependencies
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```
3. Run the notebooks in order:
   1. `obesity_visualize_clean.ipynb` — cleans the raw data and produces the EDA
   2. `Obesity_Prediction_Modeling_.ipynb` — engineers features and trains/evaluates the models
4. Open `Obesity Dashboard.pbix` in Power BI Desktop to explore the interactive dashboard
5. Review `AI_Insights_and_Recommendations_Report.pdf` for the business-facing summary

## 📈 Key Takeaways

- **Random Forest** was the top-performing model at ~99.8% test accuracy, closely followed by the Decision Tree
- **Weight and BMI** are — unsurprisingly — the strongest predictors, but **vegetable consumption frequency and number of daily meals** emerged as meaningful, actionable lifestyle signals independent of current body measurements
- **Family history of overweight** is one of the clearest single-feature signals in the dataset
- Gender shows a notable split at the extreme obesity classes, worth further investigation

## 📄 License

This project was developed for academic purposes as a Data Analytics final project.
