# SmartCart – Customer Segmentation using Clustering

## 📌 Overview

SmartCart is an unsupervised Machine Learning project that groups e-commerce customers into meaningful segments based on their demographics, purchasing behaviour, engagement levels, and loyalty indicators. The segments help the business move from generic marketing to personalised marketing and customer retention.

---

## 🎯 Problem Statement

SmartCart is a growing e-commerce platform serving customers across multiple countries. It currently uses generic marketing and engagement strategies for all customers, which leads to:

- Inefficient marketing spend
- Missed opportunities to retain high-value customers
- Delayed identification of churn-prone users

This project builds an intelligent customer segmentation system using clustering algorithms to discover hidden patterns in customer behaviour and support data-driven decision-making.

---

## 🚀 Features

- Missing Value Handling
- Feature Engineering (Age, Tenure, Total Spending, Total Children, etc.)
- Outlier Removal
- Exploratory Data Analysis (Pair Plots, Correlation Heatmap)
- Categorical Encoding (One-Hot Encoding)
- Feature Scaling (StandardScaler)
- Dimensionality Reduction (PCA) & 3D Visualization
- Optimal K Selection (Elbow Method + Silhouette Score)
- Clustering with K-Means and Agglomerative Clustering
- Cluster Profiling & Interpretation

---

## 🛠️ Technologies Used

- Python
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- KneeLocator (`kneed`)
- Jupyter Notebook

---

## 📊 Dataset

The dataset (`smartcart_customers.csv`) contains **2,240 customer records** and **22 attributes**.

**Customer Demographics**

| Feature | Description |
|---|---|
| ID | Unique customer identifier |
| Year_Birth | Year of birth of the customer |
| Education | Highest education level achieved |
| Marital_Status | Marital status of the customer |
| Income | Yearly household income |
| Kidhome | Number of small children in household |
| Teenhome | Number of teenagers in household |
| Dt_Customer | Date when customer enrolled with SmartCart |

**Purchase Behaviour (Amount Spent)**

| Feature | Description |
|---|---|
| MntWines | Amount spent on wine products |
| MntFruits | Amount spent on fruits |
| MntMeatProducts | Amount spent on meat products |
| MntFishProducts | Amount spent on fish products |
| MntSweetProducts | Amount spent on sweet products |
| MntGoldProds | Amount spent on gold products |

**Purchase Behaviour (Frequency)**

| Feature | Description |
|---|---|
| NumDealsPurchases | Purchases made using discounts |
| NumWebPurchases | Purchases made through website |
| NumCatalogPurchases | Purchases made through catalog |
| NumStorePurchases | Purchases made in physical stores |
| NumWebVisitsMonth | Number of website visits per month |

**Customer Feedback & Constants**

| Feature | Description |
|---|---|
| Recency | Number of days since last purchase |
| Complain | Customer complained in last 2 years (1 = Yes, 0 = No) |
| Response | Customer response to the last campaign (1 = Yes, 0 = No) |

---

## 🧹 Preprocessing & Feature Engineering

1. **Missing values** – 24 missing `Income` values filled with the median.
2. **New features**
   - `Age` from `Year_Birth`
   - `Customer_Tenure_Days` from `Dt_Customer`
   - `Total_Spending` = sum of all `Mnt*` columns
   - `Total_Children` = `Kidhome` + `Teenhome`
   - `Education` grouped into Undergraduate / Graduate / Postgraduate
   - `Living_With` (Partner / Alone) derived from `Marital_Status`
3. **Dropped columns** – `ID`, `Year_Birth`, `Marital_Status`, `Kidhome`, `Teenhome`, `Dt_Customer` and the individual `Mnt*` columns.
4. **Outlier removal** – `Age < 90` and `Income < 600,000` (2,240 → 2,236 records).
5. **Encoding** – One-Hot Encoding for `Education` and `Living_With`.
6. **Scaling** – `StandardScaler`.
7. **PCA** – reduced to 3 components (~45% of total variance) for clustering and 3D visualization.

---

## 🤖 Clustering Approach

| Step | Details |
|---|---|
| Choosing K | Elbow Method (with `KneeLocator`) and Silhouette Score |
| Optimal K | **4** |
| Algorithm 1 | K-Means (`n_clusters=4`) |
| Algorithm 2 | Agglomerative Clustering (`n_clusters=4`, Ward linkage) |
| Cluster profiling | Agglomerative Clustering labels |

---

## 👥 Customer Segments

Average values per cluster (from Agglomerative Clustering):

| Cluster | Living With | Avg Income | Avg Total Spending | Avg Children | Campaign Response | Web Visits / Month |
|:---:|---|---:|---:|---:|---:|---:|
| 0 | Partner | ~39.7K | ~222 | 1.24 | 7.6% | 6.3 |
| 1 | Partner | ~72.8K | ~1,237 | 0.51 | 16.7% | 3.6 |
| 2 | Alone | ~37.0K | ~166 | 1.27 | 14.2% | 6.7 |
| 3 | Alone | ~70.7K | ~1,190 | 0.46 | 32.0% | 3.7 |

**Key insights**

- **High-value segments (1 & 3):** high income, high spending, few children, heavy catalog and store purchases. They are the priority for loyalty and premium offers.
- **Cluster 3** responds best to campaigns (~32%), making it the most valuable target for marketing.
- **Budget-conscious segments (0 & 2):** lower income and spending, more children, more deal purchases and more website visits, so discount-driven campaigns suit them best.



## ▶️ How to Run

1. Clone the repository
2. Install dependencies

```bash
pip install pandas matplotlib seaborn scikit-learn kneed jupyter
```

3. Open the notebook

```bash
jupyter notebook smartcart.ipynb
```

---

## 📌 Future Improvements

- Try other algorithms (DBSCAN, Gaussian Mixture Models)
- Compare clusters using more metrics (Davies-Bouldin, Calinski-Harabasz)
- Build a churn-risk score per cluster
- Deploy as a Streamlit dashboard for the marketing team

---

## 👨‍💻 Author

Tushar Thorat

LinkedIn: *(Add your LinkedIn URL here)*

GitHub: *(Add your GitHub URL here)*
