# 📊 Marketing Campaign Analysis

> An end-to-end customer analytics project exploring the factors that drive purchasing behavior and campaign success using the 4 Ps of Marketing framework.

---

## 📁 Project Structure

```
marketing-campaign-analysis/
│
├── Marketing_Campaigns_Enhanced.ipynb   # Main analysis notebook
├── marketing_data.csv                   # Raw dataset (2,240 customers)
├── Data_Dictionary_-_Response_to_marketing_campaigns.xlsx
└── README.md
```

---

## 🎯 Objective

Analyze customer demographics, spending patterns, purchase channels, and campaign responses to derive actionable business insights for marketing strategy optimization.

---

## 📦 Dataset Overview

| Property | Value |
|---|---|
| Rows | 2,240 customers |
| Columns | 28 features |
| Source | Marketing campaign response dataset |

The dataset is organized around the **4 Ps of Marketing**:

| P | Features |
|---|---|
| **People** | Year_Birth, Education, Marital_Status, Income, Kidhome, Teenhome |
| **Product** | MntWines, MntFruits, MntMeatProducts, MntFishProducts, MntSweetProducts, MntGoldProds |
| **Place** | NumWebPurchases, NumCatalogPurchases, NumStorePurchases, NumWebVisitsMonth |
| **Promotion** | AcceptedCmp1–5, Response, Complain |

---

## 🛠️ Tech Stack

```
Python 3.x
├── pandas          — data manipulation
├── numpy           — numerical operations
├── matplotlib      — visualizations
├── seaborn         — statistical plots
├── scikit-learn    — encoding (OrdinalEncoder, get_dummies)
└── scipy.stats     — hypothesis testing (f_oneway, ttest_ind, spearmanr)
```

---

## 🔄 Analysis Pipeline

```
1. Load & Inspect Data
       ↓
2. Data Type Correction  (Income → float, Dt_Customer → datetime)
       ↓
3. Categorical Cleaning  (Education, Marital_Status standardization)
       ↓
4. Missing Value Imputation  (group-level median by Education × Marital_Status)
       ↓
5. Feature Engineering  (Age, Total_Children, Total_spendings, Total_Purchases)
       ↓
6. EDA — Distributions & Outlier Detection  (boxplots, histograms)
       ↓
7. Encoding  (Ordinal for Education, One-Hot for Marital_Status & Country)
       ↓
8. Correlation Heatmap
       ↓
9. Hypothesis Testing  (4 tests)
       ↓
10. Business Insight Visualizations
```

---

## 🧪 Hypothesis Testing Summary

Four statistical hypotheses were tested at **α = 0.05**:

### H1 — Age & In-Store Shopping
- **Test:** One-Way ANOVA (3 groups: Young / Middle / Old)
- **Why ANOVA:** Comparing means across 3+ independent groups in one test avoids inflating Type I error from multiple t-tests.
- **Result:** ✅ **Reject H₀** — F = 18.82, p ≈ 0.000
- **Finding:** Older customers (55+) make significantly more in-store purchases.

### H2 — Children & Online Shopping
- **Test:** Welch's t-test (customers with children vs. without)
- **Why Welch's:** Two independent groups with unequal sizes and unequal variances — Welch's does not assume homogeneity of variance.
- **Result:** ✅ **Reject H₀** — p < 0.05
- **Finding:** Customers with children make significantly more web purchases.

### H3 — Channel Cannibalization
- **Test:** Spearman Rank Correlation (store vs. web, store vs. catalog)
- **Why Spearman:** Purchase counts are right-skewed integers — Spearman is robust to non-normality and outliers.
- **Result:** ❌ **Fail to Reject H₀** — Positive correlations found (not negative)
- **Finding:** Channels are **complementary**, not cannibalistic — omnichannel behavior.

### H4 — US vs. Rest of World
- **Test:** Welch's t-test (US customers vs. non-US customers)
- **Why Welch's:** Two independent groups with very different sample sizes.
- **Result:** ❌ **Fail to Reject H₀** — p > 0.05
- **Finding:** The US does not significantly outperform other markets on a per-customer basis.

---

## 💡 Key Business Insights

### Product
- 🥇 **Wines** are the top revenue driver, accounting for the largest share of total spending.
- 🥩 **Meat Products** rank second — primarily purchased via catalog.
- 🍬 **Fruits & Sweets** are the lowest performers — candidates for bundle promotions.

### People
- **Income** is the strongest predictor of spending (r ≈ 0.79 with Total_spendings).
- Customers with **more children spend significantly less** — budget is redirected to childcare.
- The customer base is predominantly **middle-aged (40–70 years)** with Graduation+ education.

### Place (Channels)
- Channels are **complementary** — frequent in-store shoppers also buy more online and via catalog.
- **Customers with children prefer web** — convenience over physical shopping.

### Promotion
- **Spain (SP)** is the top market for last campaign acceptance — deserves priority budget.
- Campaign acceptance is **not strongly age-dependent** — income and product affinity are better predictors.

---

## 📋 Strategic Recommendations

| Priority | Recommendation |
|---|---|
| 1 | Focus premium wine & meat campaigns on high-income, childless customers |
| 2 | Invest in digital/web UX improvements for family segments |
| 3 | Prioritize Spain for next campaign rollout |
| 4 | Adopt an integrated omnichannel strategy — channels reinforce each other |
| 5 | Explore bundling strategies for low-revenue categories (fruits, sweets) |
| 6 | Equalize international marketing budget — US is not a dominant outlier |

---

## ⚙️ How to Run

1. **Clone / download** the project folder.
2. **Install dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn scipy openpyxl
   ```
3. **Update the data path** in Cell 3 of the notebook:
   ```python
   data = pd.read_csv("path/to/marketing_data.csv")
   ```
4. **Run all cells** top-to-bottom in Jupyter Notebook or JupyterLab.

---

## 📌 Notes

- The `Income` column required cleaning (removal of `$` and `,` symbols before conversion to float).
- 24 missing `Income` values were imputed using **group-level median** (by Education × Marital_Status).
- Extreme age outliers (customers with birth years like 1893) are present in the data — these are data entry errors and should be noted when interpreting age-based results.
- The `data_viz` copy (pre-encoding) is retained throughout for interpretable visualizations.

---

## 👤 Author

**Marketing Campaign Analysis Project**  
Submitted as part of a data analytics assignment.
