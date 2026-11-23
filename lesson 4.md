
# LESSON 4: NETFLIX DATA ANALYSIS

# 1. Importing Libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 2. Loading the Dataset
df = pd.read_csv("netflix_titles.csv")

# 3. Understanding the Dataset
print(df.head())
print(df.shape)
print(df.columns)
print(df.info())
print(df.describe())
print(df.dtypes)

# 4. Data Cleaning
print(df.isnull().sum())
print(df.duplicated().sum())

df = df.drop_duplicates()

df["director"] = df["director"].fillna("Unknown")
df["cast"] = df["cast"].fillna("Unknown")
df["country"] = df["country"].fillna("Unknown")
df["rating"] = df["rating"].fillna("Not Rated")
df["duration"] = df["duration"].fillna("Unknown")

df["date_added"] = pd.to_datetime(
    df["date_added"].str.strip(),
    errors="coerce"
)

print(df.isnull().sum())

# 5. Data Manipulation
movies = df[df["type"] == "Movie"]
tv_shows = df[df["type"] == "TV Show"]

df = df.sort_values(by="release_year", ascending=False)

df["year_added"] = df["date_added"].dt.year

df["duration_number"] = pd.to_numeric(
    df["duration"].str.extract(r"(\d+)")[0],
    errors="coerce"
)

df["duration_unit"] = df["duration"].str.extract(
    r"(min|Seasons?)",
    expand=False
)

print(df.groupby("type")["show_id"].count())

# 6. Exploratory Data Analysis (EDA)

print("Total Titles:", df["show_id"].nunique())

print("Movies and TV Shows:")
print(df["type"].value_counts())

print("Content by Release Year:")
print(df["release_year"].value_counts().sort_index())

countries = df["country"].str.split(", ").explode()
print("Top 10 Countries:")
print(countries.value_counts().head(10))

genres = df["listed_in"].str.split(", ").explode()
print("Top 10 Genres:")
print(genres.value_counts().head(10))

print("Content Ratings:")
print(df["rating"].value_counts())

print("Average Movie Duration:")
print(movies["duration_number"].mean())

print("TV Show Seasons:")
print(tv_shows["duration_number"].describe())

# 7. Data Visualization
sns.set_style("whitegrid")

# Movies vs TV Shows
sns.countplot(data=df, x="type")
plt.title("Movies vs TV Shows")
plt.xlabel("Content Type")
plt.ylabel("Number of Titles")
plt.show()

# Content Released Each Year
yearly_releases = df["release_year"].value_counts().sort_index()
yearly_releases.plot(kind="line", figsize=(10, 5))
plt.title("Netflix Content by Release Year")
plt.xlabel("Release Year")
plt.ylabel("Number of Titles")
plt.show()

# Top 10 Countries
countries.value_counts().head(10).plot(
    kind="bar", figsize=(10, 5)
)
plt.title("Top 10 Content-Producing Countries")
plt.xlabel("Country")
plt.ylabel("Number of Titles")
plt.xticks(rotation=45)
plt.show()

# Top 10 Genres
genres.value_counts().head(10).plot(
    kind="bar", figsize=(10, 5)
)
plt.title("Top 10 Netflix Genres")
plt.xlabel("Genre")
plt.ylabel("Number of Titles")
plt.xticks(rotation=45)
plt.show()

# Content Ratings
plt.figure(figsize=(10, 5))
sns.countplot(
    data=df,
    y="rating",
    order=df["rating"].value_counts().head(10).index
)
plt.title("Netflix Content Ratings")
plt.xlabel("Number of Titles")
plt.ylabel("Rating")
plt.show()

# Movie Duration Distribution
plt.figure(figsize=(10, 5))
sns.histplot(data=movies, x="duration_number", bins=30)
plt.title("Distribution of Movie Durations")
plt.xlabel("Duration in Minutes")
plt.ylabel("Frequency")
plt.show()

# 8. Final Summary
print("\nFINAL DATASET SUMMARY")

print("Total Titles:", df["show_id"].nunique())
print("Total Movies:", len(movies))
print("Total TV Shows:", len(tv_shows))
print("Most Common Content Type:", df["type"].mode()[0])
print("Most Common Release Year:", df["release_year"].mode()[0])
print("Most Common Rating:", df["rating"].mode()[0])

print(
    "Average Movie Duration:",
    round(movies["duration_number"].mean(), 2),
    "minutes"
)

print("Dataset Analysis Completed!")
