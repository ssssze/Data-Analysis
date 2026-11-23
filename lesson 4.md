
# NETFLIX MOVIES AND TV SHOWS - DATA ANALYSIS PROJECT

# 1. Importing Libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 2. Loading the Dataset
df = pd.read_csv("netflix_titles.csv")

# 3. Understanding the Dataset
print("\nDATASET OVERVIEW")
print("First five records:")
print(df.head())

print("\nDataset dimensions:")
print(df.shape)

print("\nColumn information:")
print(df.info())

print("\nStatistical summary:")
print(df.describe(include="all"))

# 4. Data Cleaning
print("\nMISSING VALUES")
print(df.isnull().sum())

print("\nDUPLICATE RECORDS")
print(df.duplicated().sum())

df = df.drop_duplicates().copy()

# Handling missing values
df["director"] = df["director"].fillna("Unknown")
df["cast"] = df["cast"].fillna("Unknown")
df["country"] = df["country"].fillna("Unknown")
df["rating"] = df["rating"].fillna("Not Rated")
df["duration"] = df["duration"].fillna("Unknown")

# Converting dates into datetime format
df["date_added"] = pd.to_datetime(
    df["date_added"].str.strip(),
    errors="coerce"
)

# Extracting numerical duration and its unit
df["duration_number"] = pd.to_numeric(
    df["duration"].str.extract(r"(\d+)")[0],
    errors="coerce"
)

df["duration_unit"] = df["duration"].str.extract(
    r"(min|Seasons?)",
    expand=False
)

print("\nMISSING VALUES AFTER CLEANING")
print(df.isnull().sum())

# 5. Data Manipulation
movies = df[df["type"] == "Movie"].copy()
tv_shows = df[df["type"] == "TV Show"].copy()

# Sorting titles by release year
df = df.sort_values(
    by="release_year",
    ascending=False
)

# Extracting the year content was added
df["year_added"] = df["date_added"].dt.year

# Separating multiple countries and genres
countries = df["country"].str.split(", ").explode()
genres = df["listed_in"].str.split(", ").explode()

# 6. Exploratory Data Analysis (EDA)

print("\nEXPLORATORY DATA ANALYSIS")

# Total number of titles
print("Total titles:", df["show_id"].nunique())

# Movies and TV shows
print("\nContent type distribution:")
print(df["type"].value_counts())

print("\nContent type percentages:")
print(df["type"].value_counts(normalize=True) * 100)

# Release year analysis
print("\nRelease year distribution:")
print(df["release_year"].value_counts().sort_index())

print("\nMost common release years:")
print(df["release_year"].value_counts().head(10))

# Country analysis
print("\nTop 10 countries:")
print(countries[countries != "Unknown"].value_counts().head(10))

# Genre analysis
print("\nTop 10 genres:")
print(genres.value_counts().head(10))

# Content rating analysis
print("\nContent ratings:")
print(df["rating"].value_counts())

# Movie duration analysis
print("\nMovie duration statistics:")
print(movies["duration_number"].describe())

print("\nAverage movie duration:")
print(movies["duration_number"].mean())

# TV show season analysis
print("\nTV show season statistics:")
print(tv_shows["duration_number"].describe())

# Content added over time
print("\nTitles added each year:")
print(df["year_added"].value_counts().sort_index())

# 7. Data Visualization
sns.set_theme(style="whitegrid")

# Movies vs TV Shows
plt.figure(figsize=(8, 5))
sns.countplot(data=df, x="type")
plt.title("Movies vs TV Shows")
plt.xlabel("Content Type")
plt.ylabel("Number of Titles")
plt.tight_layout()
plt.show()

# Content released each year
plt.figure(figsize=(12, 5))
df["release_year"].value_counts().sort_index().plot(kind="line")
plt.title("Netflix Content by Release Year")
plt.xlabel("Release Year")
plt.ylabel("Number of Titles")
plt.tight_layout()
plt.show()

# Top 10 countries
plt.figure(figsize=(10, 5))
countries[countries != "Unknown"].value_counts().head(10).plot(kind="bar")
plt.title("Top 10 Content-Producing Countries")
plt.xlabel("Country")
plt.ylabel("Number of Titles")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Top 10 genres
plt.figure(figsize=(10, 5))
genres.value_counts().head(10).plot(kind="bar")
plt.title("Top 10 Netflix Genres")
plt.xlabel("Genre")
plt.ylabel("Number of Titles")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Content ratings
plt.figure(figsize=(10, 5))
sns.countplot(
    data=df,
    y="rating",
    order=df["rating"].value_counts().head(10).index
)
plt.title("Netflix Content Ratings")
plt.xlabel("Number of Titles")
plt.ylabel("Rating")
plt.tight_layout()
plt.show()

# Movie duration distribution
plt.figure(figsize=(10, 5))
sns.histplot(
    data=movies,
    x="duration_number",
    bins=30,
    kde=True
)
plt.title("Distribution of Movie Durations")
plt.xlabel("Duration in Minutes")
plt.ylabel("Frequency")
plt.tight_layout()
plt.show()

# TV show seasons distribution
plt.figure(figsize=(8, 5))
sns.countplot(
    data=tv_shows,
    x="duration_number",
    order=sorted(tv_shows["duration_number"].dropna().unique())
)
plt.title("Distribution of TV Show Seasons")
plt.xlabel("Number of Seasons")
plt.ylabel("Number of TV Shows")
plt.tight_layout()
plt.show()

# Movie duration box plot
plt.figure(figsize=(10, 5))
sns.boxplot(data=movies, x="duration_number")
plt.title("Movie Duration and Outliers")
plt.xlabel("Duration in Minutes")
plt.tight_layout()
plt.show()

# 8. Final Summary
print("\nFINAL DATA ANALYSIS SUMMARY")

print("Total titles:", df["show_id"].nunique())
print("Total movies:", len(movies))
print("Total TV shows:", len(tv_shows))

print("Most common content type:", df["type"].mode()[0])
print("Most common release year:", df["release_year"].mode()[0])
print("Most common content rating:", df["rating"].mode()[0])

print(
    "Average movie duration:",
    round(movies["duration_number"].mean(), 2),
    "minutes"
)

print(
    "Most common genre:",
    genres.value_counts().index[0]
)

print(
    "Top country:",
    countries[countries != "Unknown"].value_counts().index[0]
)

print("\nDATA ANALYSIS COMPLETED!")

