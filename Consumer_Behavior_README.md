# 🛒 Consumer Behavior Analytics

**Business Problem Statement**  
> *How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?*

---

## 📌 Overview

This project delivers a full end-to-end analytics pipeline on consumer shopping behavior for a leading retail company. It spans Python-based data engineering, SQL business intelligence queries, Power BI visualizations, and statistical hypothesis testing — providing actionable insights into customer purchasing patterns, loyalty drivers, and revenue optimization opportunities.

---

## 🎯 Project Objectives

- Clean and prepare the consumer behavior dataset for analytical accuracy
- Organize data into a structured relational model and run SQL queries for business insights
- Build an interactive Power BI dashboard for stakeholder-ready visualizations
- Identify key purchase drivers — discounts, reviews, seasons, and payment preferences
- Apply statistical hypothesis testing and confidence intervals to validate findings
- Deliver actionable business recommendations to improve engagement and revenue
- Document all code, queries, and assets in a structured GitHub repository

---

## 🗂️ Project Pipeline

| Stage | Description | Tools |
|---|---|---|
| 1. Data Preparation & Modeling | Clean, transform, and engineer features from raw dataset | Python / Pandas |
| 2. Data Analysis (SQL) | Structured schema + business intelligence queries | sql / SQLite |
| 3. Visualization & Insights | Interactive dashboard with KPIs and trend charts | Python Libraries |
| 4. Report & Presentation | Key findings and recommendations for stakeholders | MS Word / PowerPoint |
| 5. GitHub Repository | Well-structured code repository with all assets | Git / GitHub |

---

## 📊 Dataset

**File:** `customer_shopping_behavior.csv`

Key columns used in the analysis:

| Column | Description |
|---|---|
| Age | Customer age |
| Gender | Male / Female |
| Category | Product category |
| Item Purchased | Specific product bought |
| Purchase Amount (USD) | Transaction value |
| Season | Season of purchase |
| Review Rating | Customer rating (imputed with category median) |
| Subscription Status | Whether the customer is subscribed |
| Payment Method | Payment channel used |
| Frequency of Purchases | How often the customer buys |
| Discount Applied | Whether a discount was used |
| Promo Code Used | Whether a promo code was applied |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python (Pandas, NumPy) | Data loading, cleaning, feature engineering |
| Matplotlib / Seaborn | EDA visualizations |
| SciPy | Hypothesis testing and confidence intervals |
| PostgreSQL / SQLite | SQL business queries |
| Power BI | Interactive dashboards |
| Git / GitHub | Version control and project hosting |

---

## 🔍 Exploratory Data Analysis (EDA)

Key questions answered during EDA:

- **Average purchase amount by category** — grouped bar chart
- **Which gender spends more on average?** — pie chart comparison
- **Top 5 most purchased items** — horizontal bar chart
- **Seasonal effect on purchase amount** — boxplots by season
- **Review rating distribution** — histogram with KDE
- **Most popular payment methods** — bar chart
- **Subscribers vs. non-subscribers spending** — comparative bar chart
- **Shipping type usage by purchase frequency** — stacked bar chart
- **Age group distribution of customers** — segmented bar chart

### Feature Engineering

```python
# Age group segmentation
labels = ['Young', 'Adult', 'Middle_aged', 'Senior']
df['age_group'] = pd.qcut(df['Age'], q=4, labels=labels)

# Purchase frequency in days
frequency_mapping = {
    'Weekly': 7, 'Fortnightly': 14, 'Bi-weekly': 14,
    'Monthly': 30, 'Quarterly': 90, 'Every 3 months': 90, 'Annualy': 365
}
df['purchase_frequency_days'] = df['Frequency of Purchases'].map(frequency_mapping)

# Missing value imputation
df['Review Rating'] = df.groupby('Category')['Review Rating'] \
                        .transform(lambda x: x.fillna(x.median()))
```

---

## 🧪 Hypothesis Testing & Confidence Intervals

When to use which statistical technique:

| Technique | Use When |
|---|---|
| T-Test | Comparing means of 2 groups |
| ANOVA | Comparing means of 3+ groups |
| Chi-Square Test | Comparing categorical variables |
| Confidence Interval | Estimating a population parameter with uncertainty |

### Tests Conducted

**H1 — Do male & female customers spend the same amount?**  
→ Independent Samples T-Test

```python
from scipy import stats
male = df[df["Gender"] == "Male"]["Purchase Amount (USD)"]
female = df[df["Gender"] == "Female"]["Purchase Amount (USD)"]
t_stat, p_value = stats.ttest_ind(male, female)
# p < 0.05 → Reject H0 (significant difference)
# p ≥ 0.05 → Fail to Reject H0 (no significant difference)
```

**H2 — Does purchase amount differ across all 4 seasons?**  
→ One-Way ANOVA

```python
f_stat, p_value = stats.f_oneway(spring, summer, fall, winter)
# p < 0.05 → Season significantly affects purchase amount
```

**H3 — Do subscribers spend more than non-subscribers?**  
→ One-Tailed T-Test

```python
t_stat, p_value = stats.ttest_ind(subscribed, not_subscribed, alternative="greater")
# p < 0.05 → Subscribers spend significantly MORE
```

**H4 — Is gender independent of payment method preference?**  
→ Chi-Square Test

```python
contingency_table = pd.crosstab(df["Gender"], df["Payment Method"])
chi2, p_value, dof, expected = stats.chi2_contingency(contingency_table)
# p < 0.05 → Gender and Payment Method ARE related
```

**H5 — Is discount usage related to frequency of purchase?**  
→ Chi-Square Test

```python
ct = pd.crosstab(df["Discount Applied"], df["Frequency of Purchases"])
chi2, p_value, dof, expected = stats.chi2_contingency(ct)
```

### Confidence Intervals Computed

- **CI-1:** 95% CI for Average Purchase Amount
- **CI-2:** 95% CI — Male vs. Female Spending
- **CI-3:** 95% CI for Average Review Rating

---

## 📈 SQL Business Queries

Key business questions answered via SQL:

- Revenue share and contribution by product category
- Top 5 products with highest average rating (min. 10 reviews)
- Customer segmentation — New / Returning / Loyal
- Revenue contribution by age group
- Shipping preference patterns by purchase frequency

---

## 📊 Power BI Dashboard

The interactive dashboard includes:

- KPI cards — total revenue, avg purchase, avg rating
- Revenue breakdown by category, season, and age group
- Subscriber vs. non-subscriber spend comparison
- Payment method and discount usage trends
- Customer segmentation visuals

---

## 📁 Repository Structure

```
consumer-behavior-analytics/
│
├── data/
│   └── customer_shopping_behavior.csv
│
├── notebooks/
│   └── Customer_Shopping_Behaviour.ipynb
│
├── sql/
│   └── business_queries.sql
│
├── dashboard/
│   └── Consumer_Behavior.pbix
│
├── reports/
│   ├── Executive_Summary.pdf
│   └── Presentation.pptx
│
└── README.md
```

---

## 💡 Key Business Insights

1. **Discount & Promo Impact** — Discount usage aligns directly with promo code application; toggling either affects the other.
2. **Seasonal Trends** — Purchase behavior shows seasonal variation, enabling targeted campaign planning.
3. **Subscriber Loyalty** — Subscription status is a strong signal for spending behavior and repeat purchases.
4. **Age-Based Revenue** — Specific age segments contribute disproportionately to total revenue, enabling audience targeting.
5. **Payment Preferences** — Gender may influence payment channel choice, informing checkout UX decisions.

---

## ✅ Actionable Recommendations

- Target high-frequency buyers with tiered loyalty rewards to increase average order value
- Launch seasonal promotions aligned with peak purchase periods identified through ANOVA
- Expand subscription program offerings — subscribers demonstrate higher spending intent
- Personalize marketing by age group based on revenue contribution analysis
- Optimize checkout experience for most-used payment methods per gender segment

---

## 📚 References

- Dataset: [Kaggle — Customer Shopping Behavior](https://www.kaggle.com/)
- SciPy Documentation: [scipy.stats](https://docs.scipy.org/doc/scipy/reference/stats.html)
- Seaborn Documentation: [seaborn.pydata.org](https://seaborn.pydata.org/)
