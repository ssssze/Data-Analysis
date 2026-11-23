
# ============================================================
# LESSON 4: NETFLIX MOVIES AND TV SHOWS - DATA ANALYSIS
# Dataset: netflix_titles.csv
# ============================================================

# 1. IMPORTING LIBRARIES

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme(style="whitegrid")


# ============================================================
# 2. LOADING AND UNDERSTANDING THE DATASET
# ============================================================

df = pd.read_csv("netflix_titles.csv")

print("\n========== DATASET OVERVIEW ==========")

print("Dataset shape:", df.shape)
print("Number of titles:", len(df))
print("Number of columns:", len(df.columns))

print("\nColumn names:")
print(df.columns.tolist())

print("\nFirst five records:")
print(df.head())

print("\nDataset information:")
df.info()

print("\nBasic statistical summary:")
print(df.describe(include="all"))


# ============================================================
# 3. DATA CLEANING AND DATA QUALITY
# ============================================================

print("\n========== DATA CLEANING ==========")

print("\nMissing values before cleaning:")
print(df.isnull().sum())

print("\nTotal missing values:")
print(df.isnull().sum().sum())

print("\nDuplicate records:")
print(df.duplicated().sum())

# Remove duplicate records
df = df.drop_duplicates().copy()

# Correct three movie records where duration was
# incorrectly stored in the rating column.
wrong_rating = df["rating"].astype("string").str.contains(
    r"min$",
    case=False,
    na=False
)

df.loc[wrong_rating, "duration"] = df.loc[
    wrong_rating, "rating"
]

df.loc[wrong_rating, "rating"] = np.nan

# Convert date_added into a proper date format
df["date_added"] = pd.to_datetime(
    df["date_added"].astype("string").str.strip(),
    errors="coerce"
)

# Fill missing categorical information
columns_to_fill = [
    "director",
    "cast",
    "country",
    "rating",
    "duration"
]

for column in columns_to_fill:
    df[column] = df[column].fillna("Unknown")

print("\nMissing values after cleaning:")
print(df.isnull().sum())

print("\nThe dataset has been cleaned.")
print("Remaining duplicate records:", df.duplicated().sum())


# ============================================================
# 4. CONTENT DISTRIBUTION: MOVIES VS TV SHOWS
# ============================================================

print("\n========== CONTENT DISTRIBUTION ==========")

content_counts = df["type"].value_counts()
content_percentages = df["type"].value_counts(normalize=True) * 100

print("\nNumber of Movies and TV Shows:")
print(content_counts)

print("\nPercentage distribution:")
print(content_percentages.round(2))

print(
    f"\nMovies account for "
    f"{content_percentages.get('Movie', 0):.2f}% "
    f"of all titles."
)

print(
    f"TV Shows account for "
    f"{content_percentages.get('TV Show', 0):.2f}% "
    f"of all titles."
)

plt.figure(figsize=(7, 5))
content_counts.plot(
    kind="pie",
    autopct="%1.1f%%",
    startangle=90
)
plt.title("Distribution of Movies and TV Shows")
plt.ylabel("")
plt.tight_layout()
plt.show()


# ============================================================
# 5. ANALYSIS OF RELEASE YEARS
# ============================================================

print("\n========== RELEASE YEAR ANALYSIS ==========")

release_year_counts = df["release_year"].value_counts().sort_index()

print("\nEarliest release year:", df["release_year"].min())
print("Latest release year:", df["release_year"].max())

print("\nTen most common release years:")
print(df["release_year"].value_counts().head(10))

most_common_release_year = df["release_year"].mode()[0]

print(
    "\nThe most represented release year is",
    most_common_release_year,
    "with",
    release_year_counts[most_common_release_year],
    "titles."
)

# Display the ten most represented release years
top_release_years = df["release_year"].value_counts().head(10).sort_index()

plt.figure(figsize=(11, 5))
top_release_years.plot(kind="bar")
plt.title("Ten Most Represented Release Years")
plt.xlabel("Release Year")
plt.ylabel("Number of Titles")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Display the distribution across all release years
plt.figure(figsize=(11, 5))
release_year_counts.plot(kind="line")
plt.title("Distribution of Titles Across Release Years")
plt.xlabel("Release Year")
plt.ylabel("Number of Titles")
plt.tight_layout()
plt.show()


# ============================================================
# 6. ANALYSIS OF COUNTRIES
# ============================================================

print("\n========== COUNTRY ANALYSIS ==========")

# Separate multiple countries listed in one record
country_data = df[df["country"] != "Unknown"].copy()

country_data["country"] = country_data["country"].str.split(", ")

country_data = country_data.explode("country")

country_counts = country_data["country"].value_counts()

print("\nTen most frequently listed countries:")
print(country_counts.head(10))

print(
    "\nThe country with the highest number of title listings is",
    country_counts.idxmax(),
    "with",
    country_counts.max(),
    "listings."
)

plt.figure(figsize=(11, 6))
country_counts.head(10).sort_values().plot(kind="barh")
plt.title("Top 10 Countries by Number of Netflix Title Listings")
plt.xlabel("Number of Title Listings")
plt.ylabel("Country")
plt.tight_layout()
plt.show()


# ============================================================
# 7. ANALYSIS OF GENRES
# ============================================================

print("\n========== GENRE ANALYSIS ==========")

# Separate multiple genres assigned to each title
genre_data = df[["title", "listed_in"]].copy()

genre_data["listed_in"] = genre_data["listed_in"].str.split(", ")

genre_data = genre_data.explode("listed_in")

genre_counts = genre_data["listed_in"].value_counts()

print("\nTen most common genres:")
print(genre_counts.head(10))

print(
    "\nThe most frequently listed genre is",
    genre_counts.idxmax(),
    "with",
    genre_counts.max(),
    "listings."
)

plt.figure(figsize=(11, 6))
genre_counts.head(10).sort_values().plot(kind="barh")
plt.title("Top 10 Netflix Genres")
plt.xlabel("Number of Genre Listings")
plt.ylabel("Genre")
plt.tight_layout()
plt.show()


# ============================================================
# 8. ANALYSIS OF CONTENT RATINGS
# ============================================================

print("\n========== CONTENT RATING ANALYSIS ==========")

rating_counts = df["rating"].value_counts()

print("\nContent rating distribution:")
print(rating_counts)

print("\nTen most common content ratings:")
print(rating_counts.head(10))

print(
    "\nThe most common content rating is",
    rating_counts.index[0],
    "with",
    rating_counts.iloc[0],
    "titles."
)

plt.figure(figsize=(11, 6))
rating_counts.head(10).sort_values().plot(kind="barh")
plt.title("Most Common Netflix Content Ratings")
plt.xlabel("Number of Titles")
plt.ylabel("Rating")
plt.tight_layout()
plt.show()


# ============================================================
# 9. ANALYSIS OF MOVIE DURATION
# ============================================================

print("\n========== MOVIE DURATION ANALYSIS ==========")

movies = df[df["type"] == "Movie"].copy()

# Extract numerical duration from the duration column
movies["duration_number"] = pd.to_numeric(
    movies["duration"].astype("string").str.extract(r"(\d+)")[0],
    errors="coerce"
)

movie_durations = movies["duration_number"].dropna()

print("\nNumber of movies with recorded duration:")
print(len(movie_durations))

print("\nMovie duration statistics:")
print(movie_durations.describe())

print("\nAverage movie duration:")
print(round(movie_durations.mean(), 2), "minutes")

print("\nMedian movie duration:")
print(movie_durations.median(), "minutes")

print("\nMost common movie duration:")
print(movie_durations.mode().tolist(), "minutes")

print("\nShortest movie:")
print(movie_durations.min(), "minutes")

print("\nLongest movie:")
print(movie_durations.max(), "minutes")

plt.figure(figsize=(10, 5))
plt.hist(movie_durations, bins=30, edgecolor="black")
plt.title("Distribution of Movie Durations")
plt.xlabel("Duration in Minutes")
plt.ylabel("Number of Movies")
plt.tight_layout()
plt.show()

plt.figure(figsize=(8, 5))
sns.boxplot(x=movie_durations)
plt.title("Boxplot of Movie Durations")
plt.xlabel("Duration in Minutes")
plt.tight_layout()
plt.show()


# ============================================================
# 10. ANALYSIS OF TV SHOW SEASONS
# ============================================================

print("\n========== TV SHOW SEASON ANALYSIS ==========")

tv_shows = df[df["type"] == "TV Show"].copy()

tv_shows["season_number"] = pd.to_numeric(
    tv_shows["duration"].astype("string").str.extract(r"(\d+)")[0],
    errors="coerce"
)

season_counts = tv_shows["season_number"].value_counts().sort_index()

print("\nNumber of TV Shows by season:")
print(season_counts)

print("\nMost common number of seasons:")
print(season_counts.idxmax())

print("\nNumber of shows with one season:")
print(season_counts.get(1, 0))

print("\nHighest number of seasons:")
print(season_counts.index.max())

plt.figure(figsize=(10, 5))
season_counts.plot(kind="bar")
plt.title("Number of Seasons in Netflix TV Shows")
plt.xlabel("Number of Seasons")
plt.ylabel("Number of TV Shows")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()


# ============================================================
# 11. ANALYSIS OF NETFLIX CONTENT ADDITIONS
# ============================================================

print("\n========== NETFLIX CONTENT ADDITIONS ==========")

# Extract the year in which each title was added
df["year_added"] = df["date_added"].dt.year

year_added_counts = df["year_added"].value_counts().sort_index()

print("\nNumber of titles added each year:")
print(year_added_counts)

print("\nEarliest date added:")
print(df["date_added"].min())

print("\nLatest date added:")
print(df["date_added"].max())

print(
    "\nThe year with the highest number of additions is",
    year_added_counts.idxmax(),
    "with",
    year_added_counts.max(),
    "titles."
)

plt.figure(figsize=(11, 5))
year_added_counts.plot(kind="line", marker="o")
plt.title("Number of Netflix Titles Added Each Year")
plt.xlabel("Year Added")
plt.ylabel("Number of Titles")
plt.tight_layout()
plt.show()


# ============================================================
# 12. FINAL SUMMARY OF THE ANALYSIS
# ============================================================

print("\n========== FINAL ANALYSIS SUMMARY ==========")

print("Total number of titles:", len(df))

print(
    "Total Movies:",
    (df["type"] == "Movie").sum()
)

print(
    "Total TV Shows:",
    (df["type"] == "TV Show").sum()
)

print(
    "Most common content type:",
    content_counts.idxmax()
)

print(
    "Most common release year:",
    most_common_release_year
)

print(
    "Most frequently listed country:",
    country_counts.idxmax()
)

print(
    "Most frequently listed genre:",
    genre_counts.idxmax()
)

print(
    "Most common content rating:",
    rating_counts.index[0]
)

print(
    "Average movie duration:",
    round(movie_durations.mean(), 2),
    "minutes"
)

print(
    "Most common TV show season count:",
    season_counts.idxmax()
)

print(
    "Year with the most Netflix additions:",
    year_added_counts.idxmax()
)

print("\nNetflix dataset analysis completed successfully.")


