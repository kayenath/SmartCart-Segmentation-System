
# 🛒 SmartCart Customer Segmentation Using Clustering

## 📌 Project Overview

This project applies Customer Segmentation techniques on SmartCart customer data using Unsupervised Machine Learning.

The objective is to identify groups of customers with similar purchasing behavior, demographics, and engagement patterns so that marketing teams can create personalized campaigns and improve customer retention.

The project includes:

- Data Cleaning
- Missing Value Handling
- Feature Engineering
- Exploratory Data Analysis (EDA)
- Feature Scaling
- Dimensionality Reduction using PCA
- K-Means Clustering
- Hierarchical (Agglomerative) Clustering
- Customer Segment Profiling

---

## 🎯 Business Problem

SmartCart serves thousands of customers with diverse purchasing habits.

Treating all customers similarly can lead to:

- Ineffective marketing campaigns
- Low conversion rates
- Poor customer engagement
- Increased marketing costs

Customer segmentation helps SmartCart:

✅ Understand customer behavior

✅ Create targeted promotions

✅ Improve customer retention

✅ Increase overall revenue

---

## 📊 Dataset Information

Dataset Size:

```text
2240 Customers
22 Features
```

### Key Features

| Feature | Description |
|----------|-------------|
| Income | Customer Annual Income |
| Education | Education Level |
| Marital_Status | Family Status |
| Recency | Days Since Last Purchase |
| MntWines | Amount Spent on Wine |
| MntFruits | Amount Spent on Fruits |
| MntMeatProducts | Amount Spent on Meat Products |
| MntFishProducts | Amount Spent on Fish Products |
| MntSweetProducts | Amount Spent on Sweet Products |
| MntGoldProds | Amount Spent on Gold Products |
| NumWebPurchases | Purchases via Website |
| NumCatalogPurchases | Purchases via Catalog |
| NumStorePurchases | Purchases in Store |
| Response | Campaign Acceptance |

---

# 🧹 Data Preprocessing

## Missing Value Handling

Only Income column contained missing values.

```python
df['Income'] = df['Income'].fillna(df['Income'].median())
```

Result:

```text
All missing values removed.
```

---

# ⚙ Feature Engineering

## 1. Age Creation

```python
Age = 2026 - Year_Birth
```

---

## 2. Customer Tenure

Converted customer enrollment date into tenure.

```python
Customer_Tenure_Days =
Reference_Date - Dt_Customer
```

---

## 3. Total Spending

Created overall customer spending feature.

```python
Total_Spending =
MntWines +
MntFruits +
MntMeatProducts +
MntFishProducts +
MntSweetProducts +
MntGoldProds
```

---

## 4. Children Count

```python
Children =
Kidhome + Teenhome
```

---

## 5. Family Status Simplification

Original statuses:

```text
Married
Together
Single
Divorced
Widow
Absurd
YOLO
```

Converted into:

```text
Partner
Alone
```

---

## 6. Education Consolidation

Original Education Levels:

```text
Basic
2n Cycle
Graduation
Master
PhD
```

Grouped into:

```text
UnderGraduate
Graduate
PostGraduate
```

---

# 🗑 Feature Selection

Removed unnecessary columns:

```python
ID
Year_Birth
Marital_Status
Kidhome
Teenhome
Dt_Customer

Individual spending columns
```

Final Dataset:

```text
2236 Records
15 Features
```

---

# 🔍 Outlier Detection

Outliers observed through:

```python
sns.pairplot()
```

Removed:

```python
Age > 90
Income > 600000
```

Final Dataset:

```text
2236 Customers
```

---

# 📈 Exploratory Data Analysis

Performed:

### Pair Plot

Used to identify:

- Outliers
- Relationships
- Feature distributions

### Correlation Heatmap

Used to identify:

- Highly correlated features
- Behavioral patterns

---

# 🔄 Encoding

Applied One-Hot Encoding to:

```python
Education
Living_With
```

Generated Features:

```text
Education_Graduate
Education_PostGraduate
Education_UnderGraduate
Living_With_Alone
Living_With_Partner
```

---

# 📏 Feature Scaling

Applied Standardization:

```python
StandardScaler()
```

This ensures all features contribute equally to clustering.

---

# 🔬 Principal Component Analysis (PCA)

Used PCA for:

- Dimensionality Reduction
- Visualization
- Noise Reduction

### PCA (2 Components)

Explained Variance:

```text
PC1 = 23.16%
PC2 = 11.38%
```

---

### PCA (3 Components)

Explained Variance:

```text
PC1 = 23.16%
PC2 = 11.38%
PC3 = 10.41%
```

Total Explained Variance:

```text
44.95%
```

---

# 🤖 K-Means Clustering

## Finding Optimal K

### Elbow Method

Measured WCSS values for:

```text
K = 1 to 10
```

Result:

```text
Optimal K = 4
```

---

### Silhouette Analysis

Used for cluster validation.

```python
silhouette_score()
```

Confirmed:

```text
Best K = 4
```

---

# 🌳 Hierarchical Clustering

Applied:

```python
Agglomerative Clustering
```

Parameters:

```python
n_clusters=4
linkage='ward'
```

Cluster labels generated for customer segmentation.

---

# 📊 Cluster Visualization

Visualized clusters using:

### 2D PCA Plot

### 3D PCA Plot

### Income vs Total Spending

### Cluster Distribution

---

# 👥 Customer Segmentation Results

## Cluster 0

### Family Customers with Low Spending

Characteristics:

- Living with Partner
- Moderate Income
- Low Spending
- Average Website Activity

Business Strategy:

✅ Offer coupons

✅ Bundle discounts

✅ Family promotions

---

## Cluster 1

### Elite Customers with Partner

Characteristics:

- High Income
- High Spending
- Frequent Purchases
- Strong Loyalty

Business Strategy:

✅ Loyalty Programs

✅ Premium Memberships

✅ Exclusive Offers

---

## Cluster 2

### Budget Customers Living Alone

Characteristics:

- Low Income
- Low Spending
- Price Sensitive

Business Strategy:

✅ Cashback Offers

✅ Discount Campaigns

✅ Budget-Friendly Products

---

## Cluster 3

### High-Value Independent Customers

Characteristics:

- High Income
- High Spending
- Excellent Campaign Response
- Living Alone

Business Strategy:

✅ Premium Products

✅ VIP Programs

✅ Personalized Marketing

✅ Revenue Prioritization

---

# 📊 Cluster Summary

| Cluster | Income | Spending | Response Rate | Family Type |
|----------|---------|-----------|--------------|------------|
| 0 | Low-Medium | Low | Low | Partner |
| 1 | High | Very High | Medium | Partner |
| 2 | Low | Low | Medium | Alone |
| 3 | High | Very High | High | Alone |


# Applications and Business Uses
The identified customer segments can be used for:

Targeted Marketing Campaigns
Personalized Product Recommendations
Customer Retention Strategies
Loyalty Program Design
Revenue Optimization
Customer Relationship Management
Strategic Business Decision-Making
By leveraging these customer segments, organizations can improve marketing effectiveness, increase customer satisfaction, and maximize business revenue.

---

# 🛠 Technologies Used

```text
Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-Learn
Kneed
```

---

# 🚀 Future Improvements

- DBSCAN Clustering
- Customer Lifetime Value Prediction
- RFM Analysis
- Recommendation System
- Interactive Dashboard using Streamlit
- Automated Customer Segmentation Pipeline

---

# 📚 Learning Outcomes

This project demonstrates:

✔ Data Cleaning

✔ Feature Engineering

✔ Outlier Detection

✔ Customer Analytics

✔ PCA

✔ K-Means Clustering

✔ Agglomerative Clustering

✔ Marketing Segmentation

✔ Business Insights Generation

---

# 👨‍💻 Author

**Kayenath**

Layer-1 Technical Support Engineer | Aspiring Data Scientist & AI Engineer

GitHub: https://github.com/kayenath

---

⭐ If you found this project useful, please consider starring the repository.

