# Customer Churn Analysis — Exploratory Data Analysis

An exploratory data analysis project investigating **which customer characteristics and behaviors are associated with subscription churn**.

The analysis examines customer demographics, income, spending behavior, purchasing frequency, membership levels, and engineered behavioral features to identify patterns that can inform a future churn-prediction model.

---

## 📌 Project Overview

A subscription-based company is experiencing customer churn and wants to understand **who is most likely to leave** before developing a machine-learning churn prediction model.

This project performs a structured EDA on **2,000 customer records** and focuses on identifying actionable patterns in customer behavior.

The analysis answers questions such as:

* What does the customer base look like?
* How prevalent is churn?
* Do age, gender, or income meaningfully differentiate churned customers?
* Does membership level relate to churn?
* How do spending behavior and purchase frequency differ between retained and churned customers?
* Which customer segments have the highest churn risk?
* Which engineered features provide useful additional insight?
* What should the data science team investigate when developing the churn-prediction model?

---

## 🎯 Objectives

The analysis follows six major stages:

1. **Load & Audit the Data**

   * Dataset shape and structure
   * Data types
   * Missing values
   * Duplicate records
   * Memory usage
   * Basic descriptive statistics

2. **Univariate Analysis**

   * Explore individual customer characteristics
   * Examine distributions and category frequencies
   * Understand the composition of the customer base

3. **Bivariate Analysis**

   * Compare customer characteristics against churn status
   * Identify variables that distinguish retained and churned customers

4. **Missing Data & Outlier Analysis**

   * Identify potential outliers
   * Separate unusual observations from erroneous observations
   * Document the reasoning behind outlier treatment

5. **Feature Engineering**

   * Create 10 additional customer-behavior features
   * Develop meaningful customer segments
   * Examine whether engineered features provide stronger churn differentiation

6. **Insights & Storytelling**

   * Translate analytical findings into business insights
   * Identify high-risk and low-risk customer segments
   * Provide recommendations for future churn analysis

---

## 📊 Dataset

The dataset contains:

* **2,000 customer records**
* **9 original features**
* **1 target variable**

### Key Variables

| Feature              | Description                                    |
| -------------------- | ---------------------------------------------- |
| `CustomerID`         | Unique customer identifier                     |
| `Name`               | Customer name                                  |
| `Age`                | Customer age                                   |
| `Gender`             | Customer gender                                |
| `Annual_Income`      | Annual customer income                         |
| `Spending_Score`     | Customer spending score                        |
| `Membership_Level`   | Customer membership tier                       |
| `Purchase_Frequency` | Frequency of customer purchases                |
| `Churn_Status`       | Churn indicator: `0 = Retained`, `1 = Churned` |

> **Note:** `Spending_Score` and `Purchase_Frequency` are treated as behavioral measures provided by the dataset. The analysis focuses on how these measures differ across churn groups rather than assuming a specific real-world calculation behind the original scores.

---

# 🔎 Key Findings

The analysis found that **behavioral characteristics provide substantially stronger differentiation of churn than demographic, income, or membership characteristics**.

The overall observed churn rate is:

### **33.25%**

Several particularly strong patterns emerged.

### 1. Engagement is strongly associated with churn

Customers in the **Low Engagement** segment have a:

**71.62% churn rate**

compared with:

**14.26%**

among highly engaged customers.

This represents a **57.36 percentage-point difference**, making engagement one of the clearest broad behavioral signals in the analysis.

---

### 2. Low-frequency customers are at substantially higher risk

| Purchase Frequency | Churn Rate |
| ------------------ | ---------: |
| Low                | **55.65%** |
| Medium             | **29.09%** |
| High               | **19.66%** |

Churn decreases progressively as purchase frequency increases.

This suggests that declining purchasing activity may be useful as an early warning signal for retention teams.

---

### 3. Spending shows a similar pattern

| Spending Segment | Churn Rate |
| ---------------- | ---------: |
| Low              | **49.18%** |
| Medium           | **32.93%** |
| High             | **17.66%** |

Customers with lower spending activity show substantially higher observed churn than high-spending customers.

---

### 4. The highest-risk segment is Low Spending + Low Frequency

The strongest segmentation result in the analysis is:

> **Low Spending + Low Frequency → 98.46% churn**

This identifies an exceptionally high-risk customer population and suggests that customers exhibiting both behaviors should receive particular attention in future retention analysis.

---

### 5. High Spending + High Frequency customers are exceptionally stable

At the opposite end of the behavioral spectrum:

> **High Spending + High Frequency → 4.30% churn**

Compared with the overall churn rate of **33.25%**, this represents a dramatically lower observed churn rate.

The contrast between these two groups provides the clearest evidence that customer behavior is closely associated with observed churn in this dataset.

---

### 6. Demographics provide weaker differentiation

Age distributions for retained and churned customers are highly similar.

Gender also shows relatively limited separation:

| Gender | Churn Rate |
| ------ | ---------: |
| Female |     35.02% |
| Male   |     31.52% |

The difference is approximately **3.5 percentage points**, considerably smaller than the differences observed for behavioral variables.

---

### 7. Income provides little practical differentiation

| Income Segment | Churn Rate |
| -------------- | ---------: |
| Low            |     34.00% |
| Middle         |     33.30% |
| High           |     32.40% |

The total difference between the highest and lowest segments is only **1.60 percentage points**.

Income therefore appears substantially weaker than behavioral characteristics for churn segmentation.

---

### 8. Membership level alone provides little differentiation

| Membership Level | Churn Rate |
| ---------------- | ---------: |
| Basic            |     34.13% |
| Silver           |     31.53% |
| Gold             |     34.22% |
| Platinum         |     33.22% |

The difference between the highest and lowest membership-level churn rates is only **2.69 percentage points**.

This suggests that membership tier alone should not be treated as the primary basis for identifying churn risk.

---

# 🧹 Data Quality & Outlier Treatment

The dataset was audited before analysis.

### Data quality

* **2,000 records**
* **No missing values**
* **No duplicate rows**
* `CustomerID` values are unique
* All expected variables are present

### Outlier analysis

The IQR method identified **9 potential Annual Income outliers**:

* 4 below the lower bound
* 5 above the upper bound

The calculated bounds were:

* Lower bound: **$20,099**
* Upper bound: **$99,351**

The flagged observations were manually inspected.

They represented plausible customer income values rather than obvious data-entry errors, so **no income observations were removed**.

This distinction is important: a statistical outlier is not automatically an erroneous observation.

---

# 🧠 Feature Engineering

Ten new features were created to provide additional ways of understanding customer behavior.

Important engineered features include:

* `Engagement_Score`
* `Spending_Frequency_Gap`
* `Purchase_Frequency_Level`
* `Spending_Segment`
* `Engagement_Segment`
* `Membership_Score`
* `Customer_Behavior_Type`
* `Income_Segment`
* `Engagement_vs_Membership`
* `Customer_Value_Profile`

These features were designed to transform individual measurements into more interpretable behavioral indicators and customer segments.

The most useful patterns emerged from **engagement, spending, purchase frequency, and combined behavioral segmentation**.

Not every engineered feature provided equally strong churn differentiation, which is itself an important analytical finding.

---

# 📈 Visual Analysis

The project contains extensive visualization covering:

* Customer age distribution
* Income distribution
* Spending distribution
* Purchase-frequency distribution
* Gender composition
* Membership composition
* Overall churn distribution
* Age vs. churn
* Income vs. churn
* Spending vs. churn
* Purchase frequency vs. churn
* Engagement vs. churn
* Spending segments vs. churn
* Purchase-frequency segments vs. churn
* Engagement segments vs. churn
* Customer behavior types vs. churn
* Customer value profiles vs. churn

The notebook contains the complete exploratory visualization set, while the final EDA report selects the visualizations that best communicate the business story.

---

# 💼 Business Implications

The analysis suggests that customer retention efforts should focus primarily on **behavioral signals rather than demographic characteristics**.

Potential areas for further investigation include:

* Monitoring declining purchase frequency
* Identifying customers with consistently low spending
* Using engagement as an early-warning indicator
* Prioritizing low-spending, low-frequency customers for retention analysis
* Understanding what differentiates highly active customers from inactive customers
* Combining behavioral features when developing churn-risk segments

These findings describe **associations rather than causal relationships**. Further statistical analysis and predictive modeling are required to determine which variables provide independent predictive value.

---

# 🤖 Next Step: Churn Prediction

This EDA is intended to serve as a foundation for the next stage of the project: developing a **customer churn-prediction model**.

The data science team can use the exploratory findings to investigate behavioral and engineered features such as:

* Engagement
* Spending
* Purchase frequency
* Customer behavior type
* Customer value
* Other validated engineered features

The predictive modeling stage should evaluate whether these variables retain their predictive value when considered simultaneously.

---

# 📁 Repository Structure

```text
customer-churn-analysis/
│
├── data/
│   └── customer_churn.csv
│
├── notebook/
│   └── customer_churn_eda.ipynb
│
├── report/
│   ├── main.tex
│   ├── customer_churn_report.pdf
│   └── figures/
│       ├── ...
│
├── README.md
└── requirements.txt
```

> File and folder names may vary depending on the final repository structure.

---

# 🛠️ Tools & Technologies

* **Python**
* **Pandas** — data manipulation and analysis
* **NumPy** — numerical operations
* **Matplotlib** — visualization
* **Seaborn** — statistical visualization
* **Jupyter Notebook** — analysis environment
* **LaTeX** — business EDA report generation

---

# ▶️ Running the Project

### 1. Clone the repository

```bash
git clone <repository-url>
cd customer-churn-analysis
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the EDA notebook and run the cells **from top to bottom**.

---

# 📄 Deliverables

This repository contains:

* **Jupyter Notebook** — complete, commented, reproducible EDA
* **EDA Report** — concise business-facing report with selected visualizations
* **Figures** — visual assets used in the report
* **Data-cleaning and outlier analysis**
* **Churn-rate analysis by important customer groups**
* **10 engineered customer features**
* **10 business insights**

---

# ⚠️ Analytical Disclaimer

This project is an **exploratory analysis**, not a causal study or deployed churn-prediction system.

Observed differences between customer groups indicate associations in this dataset. They do not establish that a particular customer characteristic directly causes churn.

The next stage should validate these findings using statistical analysis and predictive modeling.

---

## Author

**Izhan Nasir**

*Data Science / Artificial Intelligence*

---

## ⭐ Project Takeaway

> **The clearest churn signal in this dataset is behavioral: customers with low engagement, low spending, and low purchase frequency are substantially more likely to churn, while highly active customers show much lower observed churn.**

The strongest contrast is between **Low Spending–Low Frequency customers (98.46% churn)** and **High Spending–High Frequency customers (4.30% churn)**, suggesting that future churn modeling should place particular attention on customer engagement and purchasing behavior.
