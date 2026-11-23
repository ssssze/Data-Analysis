
# =====================================================
# LESSON 1: UNDERSTANDING AND ANALYSING DATA
# =====================================================

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns


# =====================================================
# 1. UNDERSTAND THE DATA FIRST
# EXPLORATORY PHASE
# =====================================================

# Sample dataset for analysis

data = {
    "Month": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
    "Region": ["North", "South", "North", "East", "South", "East"],
    "Sales": [1200, 1500, 1800, 1600, 2000, 2200],
    "Expenses": [500, 600, 700, 650, 800, 850],
    "Customers": [100, 130, 150, 140, 170, 190]
}

df = pd.DataFrame(data)


# A. Check structure and size

print("\n--- DATA STRUCTURE AND SIZE ---")

print("Dataset:")
print(df)

print("\nNumber of rows and columns:")
print(df.shape)

print("\nColumn names:")
print(df.columns.tolist())

print("\nData types:")
print(df.dtypes)

print("\nDataset information:")
df.info()


# B. Spot quality issues

print("\n--- DATA QUALITY CHECK ---")

print("Missing values:")
print(df.isnull().sum())

print("\nDuplicate entries:")
print(df.duplicated().sum())

print("\nUnique values:")
print(df.nunique())

print("\nCheck numerical outliers:")
print(df[["Sales", "Expenses", "Customers"]].describe())


# C. Summarize distributions

print("\n--- DATA DISTRIBUTION ---")

print("Mean:")
print(df[["Sales", "Expenses", "Customers"]].mean())

print("\nMedian:")
print(df[["Sales", "Expenses", "Customers"]].median())

print("\nMinimum:")
print(df[["Sales", "Expenses", "Customers"]].min())

print("\nMaximum:")
print(df[["Sales", "Expenses", "Customers"]].max())

print("\nValue counts:")
print(df["Region"].value_counts())


# =====================================================
# 2. CORE ANALYSIS TECHNIQUES
# =====================================================


# A. Trends over time

print("\n--- TRENDS OVER TIME ---")

print(df[["Month", "Sales"]])

plt.figure(figsize=(8, 5))

plt.plot(df["Month"], df["Sales"], marker="o")

plt.title("Sales Trends Over Time")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.grid(True)

plt.tight_layout()
plt.show()


# B. Comparisons and segmentation

print("\n--- COMPARISONS AND SEGMENTATION ---")

region_analysis = df.groupby("Region").agg({
    "Sales": "sum",
    "Expenses": "sum",
    "Customers": "sum"
})

print(region_analysis)

plt.figure(figsize=(8, 5))

sns.barplot(
    data=df,
    x="Region",
    y="Sales",
    errorbar=None
)

plt.title("Sales Comparison by Region")
plt.xlabel("Region")
plt.ylabel("Sales")

plt.tight_layout()
plt.show()


# C. Relationships and correlation

print("\n--- RELATIONSHIPS AND CORRELATION ---")

correlation = df[["Sales", "Expenses", "Customers"]].corr()

print(correlation)

# Scatter plot

plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="Expenses",
    y="Sales"
)

plt.title("Expenses vs Sales")
plt.xlabel("Expenses")
plt.ylabel("Sales")

plt.tight_layout()
plt.show()

# Correlation heatmap

plt.figure(figsize=(7, 5))

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm"
)

plt.title("Correlation Heatmap")

plt.tight_layout()
plt.show()


# D. Anomaly detection

print("\n--- ANOMALY DETECTION ---")

Q1 = df["Sales"].quantile(0.25)
Q3 = df["Sales"].quantile(0.75)

IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

anomalies = df[
    (df["Sales"] < lower_limit) |
    (df["Sales"] > upper_limit)
]

print("Unusual records:")
print(anomalies)

print("Number of unusual records:", len(anomalies))


# =====================================================
# 3. PRACTICAL HABITS FOR ACCURATE RESULTS
# =====================================================


# A. Start with a clear question

print("\n--- ANALYSIS QUESTIONS ---")

questions = [
    "Which month has the highest sales?",
    "Which region generates the most sales?",
    "Is there a relationship between expenses and sales?",
    "Are there any unusual sales values?"
]

for question in questions:
    print("-", question)


# B. Visualize early

print("\n--- DATA VISUALIZATION ---")

# Bar chart

df.groupby("Region")["Sales"].sum().plot(
    kind="bar",
    figsize=(8, 5),
    title="Total Sales by Region"
)

plt.xlabel("Region")
plt.ylabel("Sales")
plt.tight_layout()
plt.show()


# Line graph

plt.figure(figsize=(8, 5))

plt.plot(df["Month"], df["Sales"], marker="o")

plt.title("Monthly Sales")
plt.xlabel("Month")
plt.ylabel("Sales")

plt.tight_layout()
plt.show()


# Scatter plot

plt.figure(figsize=(8, 5))

plt.scatter(df["Expenses"], df["Sales"])

plt.title("Expenses and Sales Relationship")
plt.xlabel("Expenses")
plt.ylabel("Sales")

plt.tight_layout()
plt.show()


# C. Question assumptions

print("\n--- QUESTIONING ASSUMPTIONS ---")

print("Correlation:", correlation.loc["Expenses", "Sales"])

print(
    "Remember: Correlation does not prove causation."
)

print(
    "Other factors may influence the relationship "
    "between expenses and sales."
)


# =====================================================
# END OF LESSON 1
# =====================================================

print("\nLesson 1 completed successfully!")


