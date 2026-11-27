# Statistical Analysis: Digital Habits & Mental Wellbeing

## 📌 Project Overview
This project investigates the statistical relationship between daily social media habits and mental wellbeing indicators (`N = 481` survey respondents). Rather than treating screen time as a single metric, this analysis separates **passive duration** (`daily_screen_time`) from **psychological engagement patterns** (`social_comparison`, `restlessness`, `purposeless_use`) using non-parametric inference, robust regression, and logistic risk modeling.

---


## 🎯 Problem Statement
Public discourse around digital wellbeing often reduces mental health risks to a single metric: **total daily screen time**. However, treating all screen exposure as equal overlooks *how* individuals interact with digital platforms. 

This study addresses two core questions using survey data (`N = 481` respondents):
1. Does raw daily social media duration independently drive mental distress, or do **psychological engagement patterns** (upward social comparison, restlessness, purposeless scrolling) explain the relationship?
2. Which demographic segments face the highest vulnerability to digital-related distress?

---

## 💡 How We Solved It (Analytical Workflow)
1. **Psychometric Scale Engineering (`01_data_cleaning.ipynb`):** Standardized 21 survey items, converted categorical usage intervals into numeric midpoint hours (`daily_screen_time`), and constructed a 5-item composite **Mental Distress Index** (`5–25` scale, validated via **Cronbach's α**).
2. **Non-Parametric Assumption Testing (`02_exploratory_analysis.ipynb`):** Audited skewness via Q-Q plots and Shapiro-Wilk tests, selecting rank-based **Spearman correlations (ρ)** and **Kruskal-Wallis H-tests** with Bonferroni post-hoc corrections.
3. **Multivariable Risk Modeling (`03` & `04` Notebooks):** Isolated independent behavioral predictors using **HC3 robust OLS regression** and **Binomial Logistic Regression** to estimate **Adjusted Odds Ratios (OR)** with 95% confidence intervals.

---

## 🔎 Key Observations
* **Non-Linear Jump Across Usage Tiers:** Median mental distress rises sharply from **13.0** (`Low <2h/day`) to **18.0** (`Moderate 2–5h/day`), with a smaller incremental rise to **19.0** (`High >5h/day`).
* **The "Behavior Over Hours" Inversion:** While bivariate trend lines show distress rising with screen time, controlling for behavioral habits in multivariable logistic regression renders raw `daily_screen_time` statistically non-significant (**Adjusted OR = 1.16**, 95% CI crosses `1.0`).
* **Primary Psychological Drivers:** **Upward social comparison** (**OR ≈ 1.75**, 95% CI: 1.49–2.07), **restlessness** (**OR ≈ 1.43**), and **purposeless scrolling** (**OR ≈ 1.41**) remain highly significant independent predictors of elevated distress.
* **Demographic Vulnerability:** **University Students** report the highest median distress (**18.0**), followed by **School Students** (**16.0**) and **Salaried Workers** (**14.0**), with older age acting as a modest protective factor (**OR ≈ 0.95**/year).


---

## 🔍 Key Statistical Findings

1. **Behavior Matters More Than Raw Screen Hours:**
   * In bivariate analysis, `daily_screen_time` correlates positively with `mental_distress_score`, rising from a predicted mean of **~13.0** (`<1h/day`) to **~19.0** (`>5h/day`).
   * However, in multivariable logistic regression controlling for behavioral habits, raw `daily_screen_time` becomes statistically non-significant (**Adjusted OR = 1.16**, 95% CI crosses `1.0`), whereas **upward social comparison** (**OR ≈ 1.75**, 95% CI: 1.49–2.07), **restlessness** (**OR ≈ 1.43**), and **purposeless scrolling** (**OR ≈ 1.41**) remain strong independent predictors of high mental distress.

2. **Significant Jump Across Digital Usage Tiers:**
   * Median `mental_distress_score` (composite 5–25 scale) increases significantly across usage tiers:
     * **Low (<2h/day):** Median = **13.0** (IQR: 9.0–17.0)
     * **Moderate (2–5h/day):** Median = **18.0** (IQR: 14.0–20.0)
     * **High (>5h/day):** Median = **19.0** (IQR: 16.0–22.0)

3. **Demographic & Life-Stage Disparities:**
   * **University Students** experience the highest median mental distress (**18.0**, IQR: 15.0–21.0), followed by **School Students** (**16.0**, IQR: 13.0–20.0), while **Salaried Workers** report the lowest (**14.0**, IQR: 10.0–17.25).
   * Older age acts as a modest protective factor (**OR ≈ 0.95** per year) and correlates negatively with distraction (\(\rho = -0.26\)) and worry scores (\(\rho = -0.24\)).

4. **Strong Cognitive-Emotional Clustering:**
   * Spearman rank correlations reveal tight clustering between attention fragmentation and emotional distress, led by `easily_distracted` vs. `concentration_diff` (\(\rho = 0.67\)), `easily_distracted` vs. `distracted_busy` (\(\rho = 0.60\)), and `worries_score` vs. `depression_score` (\(\rho = 0.58\)).

---

## 📊 Visual Highlights

| Usage Tiers & Distress Distribution | Multivariate Odds Ratios (Forest Plot) |
| :---: | :---: |
| ![Wellbeing by Usage Tier](reports/figures/03_wellbeing_by_usage_tier.png) | ![Odds Ratios Forest Plot](reports/figures/06_odds_ratios_forest_plot.png) |

| Spearman Correlation Matrix | Distress by Occupation Status |
| :---: | :---: |
| ![Correlation Heatmap](reports/figures/02_correlation_heatmap.png) | ![Distress by Occupation](reports/figures/05_distress_by_occupation.png) |

---


## ✅ Conclusions & Practical Implications
* **Screen-Time Limits Alone Are Insufficient:** Digital wellbeing interventions and app-level nudges focused strictly on reducing total screen hours miss the primary psychological mechanism—**passive, comparison-driven consumption**.
* **Targeted Campus Support:** Because university students experience significantly higher distress scores than working adults, institutional mental health programs should prioritize healthy digital literacy and active-vs-passive usage awareness among college cohorts.

---

## 🚀 Future Scope & Limitations
* **Cross-Sectional & Self-Report Bias:** Because survey responses are self-reported at a single point in time, causal direction cannot be definitively established (e.g., preexisting anxiety may drive higher social media escapism).
* **Objective Telemetry Integration:** Future iterations can pair longitudinal digital-wellbeing logs (objective screen-time APIs and notification frequency) with validated clinical scales (PHQ-9 / GAD-7) to test causal lagged effects.


---


## 📂 Repository Structure

```text
statistical-analysis-digital-habits-mental-wellbeing/
├── data/
│   ├── raw/                  # Raw survey dataset (excluded from Git via .gitignore)
│   └── processed/            # Cleaned dataset with engineered features
│       └── cleaned_wellbeing_data.csv
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_hypothesis_testing.ipynb
│   ├── 04_multivariate_and_segmentation.ipynb
│   └── output/               # Generated figures (01 through 06)
├── .gitignore
├── README.md
└── requirements.txt
```

---

## 🛠️ Methodology & Notebook Breakdown

* **`01_data_cleaning.ipynb`**: Standardized 21 survey questions into `snake_case`, normalized free-text gender labels, audited IQR outliers, converted text usage intervals into numeric midpoint hours (`daily_screen_time`), and constructed the composite `mental_distress_score` (sum of `worries_score`, `concentration_diff`, `depression_score`, `interest_fluctuation`, and `sleep_issues_score`).
* **`02_exploratory_analysis.ipynb`**: Assessed skewness via histograms, KDE curves, and Q-Q plots; generated Spearman rank correlation matrices, tier boxplots, and bivariate linear regression trends.
* **`03_hypothesis_testing.ipynb`**: Conducted Shapiro-Wilk normality tests, Spearman rank correlations ($\rho$), Kruskal-Wallis H-tests with $\epsilon^2$ effect sizes, Bonferroni-corrected Mann-Whitney U post-hoc tests, and `HC3` robust Ordinary Least Squares (OLS) regression.
* **`04_multivariate_and_segmentation.ipynb`**: Evaluated internal consistency reliability using Cronbach's $\alpha$, stratified distress across occupation status and individual social media platforms, and estimated Adjusted Odds Ratios (95% CI) via Binomial Logistic Regression.

---

## 🚀 How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone https://github.com
   cd statistical-analysis-digital-habits-mental-wellbeing
   ```

2. **Create and activate the virtual environment:**
   ```bash
   python -m venv venv
   # Windows (PowerShell):
   .\venv\Scripts\Activate.ps1
   # Mac / Linux:
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the notebooks in numerical order (`01` → `04`)** using Jupyter Notebook or VS Code.
