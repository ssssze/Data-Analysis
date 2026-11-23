
# LESSON 1: UNDERSTANDING AND ANALYSING DATA

## Objective
Learn how to explore datasets, identify data quality issues, analyse trends, compare categories, find relationships, detect anomalies and draw meaningful insights.

## Libraries
```bash
pip install pandas numpy matplotlib seaborn
```

## 1. Import Libraries and Create a Dataset

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Create a sample tourism dataset

data = {
    "Month": [
        "January", "February", "March", "April",
        "May", "June", "July", "August",
        "September", "October", "November", "December"
    ],

    "Region": [
        "Paro", "Thimphu", "Punakha", "Paro",
        "Thimphu", "Punakha", "Paro", "Thimphu",
        "Punakha", "Paro", "Thimphu", "Punakha"
    ],

    "Tourists": [
        1200, 1500, 1800, 1600, 2000, 2200,
        2500, 2800, 2100, 1900, 1700, 3000
    ],

    "Advertising": [
        500, 600, 700, 650, 800, 850,
        900, 1000, 750, 700, 650, 1100
    ],

    "Bookings": [
        100, 130, 150, 140, 170, 190,
        210, 240, 180, 160, 150, 260
    ]
}

df = pd.DataFrame(data)


# 2. UNDERSTANDING THE DATA

print("\n--- DATASET ---")
print(df)

# Check the first five rows
print("\nFirst five rows:")
print(df.head())

# Check the last five rows
print("\nLast five rows:")
print(df.tail())

# Check dataset size
print("\nDataset shape:")
print(df.shape)

# Check column names
print("\nColumn names:")
print(df.columns)

# Check data types
print("\nData types:")
print(df.dtypes)

# General information
print("\nDataset information:")
df.info()


# 3. IDENTIFYING DATA QUALITY ISSUES

# Check missing values
print("\n--- MISSING VALUES ---")
print(df.isnull().sum())

# Check duplicate records
print("\n--- DUPLICATES ---")
print(df.duplicated().sum())

# Check unique values
print("\n--- UNIQUE VALUES ---")
print(df.nunique())

# Check for unrealistic values
print("\n--- TOURIST ARRIVALS ---")
print(df["Tourists"].describe())


# 4. SUMMARIZING DATA DISTRIBUTIONS

print("\n--- STATISTICAL ANALYSIS ---")

print("Mean:", df["Tourists"].mean())

print("Median:", df["Tourists"].median())

print("Minimum:", df["Tourists"].min())

print("Maximum:", df["Tourists"].max())

print("Range:",
      df["Tourists"].max() - df["Tourists"].min())

print("Standard deviation:", df["Tourists"].std())

print("\nComplete statistical summary:")
print(df.describe())


# 5. TRENDS OVER TIME

print("\n--- MONTHLY TOURISM TRENDS ---")

print(df[["Month", "Tourists"]])

# Create a line graph
plt.figure(figsize=(10, 5))

plt.plot(
    df["Month"],
    df["Tourists"],
    marker="o"
)

plt.title("Monthly Tourist Arrivals")
plt.xlabel("Month")
plt.ylabel("Number of Tourists")

plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()


# 6. COMPARISONS AND SEGMENTATION

# Group tourist arrivals by region

region_analysis = df.groupby("Region")["Tourists"].agg(
    ["sum", "mean", "max", "min"]
)

print("\n--- REGIONAL ANALYSIS ---")
print(region_analysis)

# Compare regions using a bar chart

plt.figure(figsize=(8, 5))

sns.barplot(
    data=df,
    x="Region",
    y="Tourists",
    estimator="sum",
    errorbar=None
)

plt.title("Total Tourist Arrivals by Region")
plt.xlabel("Region")
plt.ylabel("Total Tourists")

plt.tight_layout()
plt.show()


# 7. RELATIONSHIPS AND CORRELATION

# Calculate correlation between advertising and bookings

correlation = df["Advertising"].corr(df["Bookings"])

print("\n--- CORRELATION ANALYSIS ---")
print("Correlation:", correlation)

# Create a scatter plot

plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="Advertising",
    y="Bookings"
)

plt.title("Advertising Expenses vs Bookings")
plt.xlabel("Advertising Expenses")
plt.ylabel("Bookings")

plt.tight_layout()
plt.show()

# Correlation heatmap

plt.figure(figsize=(7, 5))

sns.heatmap(
    df[["Tourists", "Advertising", "Bookings"]].corr(),
    annot=True,
    cmap="coolwarm",
    vmin=-1,
    vmax=1
)

plt.title("Correlation Heatmap")
plt.tight_layout()
plt.show()


# 8. ANOMALY DETECTION

# Use the IQR method to identify unusual values

Q1 = df["Tourists"].quantile(0.25)
Q3 = df["Tourists"].quantile(0.75)

IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

# Identify anomalies

anomalies = df[
    (df["Tourists"] < lower_limit) |
    (df["Tourists"] > upper_limit)
]

print("\n--- ANOMALY DETECTION ---")
print(anomalies)

print("Number of unusual records:", len(anomalies))


# 9. DATA VISUALIZATION

# Histogram: Distribution of tourist arrivals

plt.figure(figsize=(8, 5))

sns.histplot(
    df["Tourists"],
    bins=6,
    kde=True
)

plt.title("Distribution of Tourist Arrivals")
plt.xlabel("Number of Tourists")
plt.ylabel("Frequency")

plt.tight_layout()
plt.show()


# Boxplot: Identify unusual values visually

plt.figure(figsize=(8, 5))

sns.boxplot(
    x=df["Tourists"]
)

plt.title("Tourist Arrivals Boxplot")
plt.xlabel("Number of Tourists")

plt.tight_layout()
plt.show()


# 10. FINAL ANALYSIS AND INSIGHTS

print("\n========== FINAL ANALYSIS ==========")

print("Total tourist arrivals:",
      df["Tourists"].sum())

print("Average tourist arrivals:",
      round(df["Tourists"].mean(), 2))

print("Highest tourist arrivals:",
      df["Tourists"].max())

print("Lowest tourist arrivals:",
      df["Tourists"].min())

print("Month with highest arrivals:",
      df.loc[df["Tourists"].idxmax(), "Month"])

print("Region with highest total arrivals:",
      region_analysis["sum"].idxmax())

print("Advertising and bookings correlation:",
      round(correlation, 2))

print("Number of unusual records:",
      len(anomalies))

print("\nData analysis completed successfully!")
```

## 11. Important Concepts Learned

| Topic | Skills |
|---|---|
| Exploratory analysis | Dataset structure, size and data types |
| Data quality | Missing values and duplicates |
| Statistics | Mean, median, range and standard deviation |
| Trends | Changes over time |
| Comparisons | Grouping and segmentation |
| Correlation | Relationships between variables |
| Anomalies | Identifying unusual records |
| Visualization | Line graphs, bar charts, histograms and scatter plots |
| Interpretation | Drawing meaningful conclusions |

## 12. Important Notes

- Always understand your dataset before performing analysis.
- Start with a clear question.
- Visualize your data to identify patterns.
- Check unusual values before making conclusions.
- Correlation does not necessarily mean causation.
- Do not assume that every unusual value is an error.

## Learning Goal

By completing this lesson, I aim to understand how to explore, analyse and interpret datasets and turn raw data into meaningful insights.



