
# Lesson 4: Real-World Data Analysis – Netflix Movies and TV Shows

## 1. Introduction

For this lesson, I analysed the Netflix Movies and TV Shows dataset from Kaggle, created by Shivam Bansal. The purpose of this analysis is to understand the contents of the dataset, identify patterns and trends, compare different categories and discover useful information through data analysis.

The dataset contains **8,807 records and 12 columns**. Each record represents a movie or TV show and includes information such as its title, director, cast, country of production, release year, rating, duration, genre and description.

It is important to note that the dataset represents Netflix titles recorded up to September 2021. Therefore, it does not necessarily represent Netflix's current catalogue.

## 2. Understanding the Dataset

The dataset contains twelve columns, each providing a different type of information about the titles.

- **Show ID:** A unique identification number assigned to each title.
- **Type:** Identifies whether the content is a Movie or a TV Show.
- **Title:** Contains the name of each movie or TV show.
- **Director:** Provides information about the director of the title.
- **Cast:** Lists the actors and performers involved.
- **Country:** Shows the country or countries where the content was produced.
- **Date Added:** Records when the title was added to Netflix.
- **Release Year:** Indicates the year the movie or TV show was originally released.
- **Rating:** Provides the age-based content classification.
- **Duration:** Records the running time of movies or the number of seasons in TV Shows.
- **Listed In:** Contains the genres and categories assigned to each title.
- **Description:** Provides a short summary of the content.

Understanding these columns is important because it helps determine what information is available and what types of analysis can be performed.

## 3. Data Cleaning and Quality

Before analysing the dataset, I examined its structure, checked for missing values and searched for duplicate records.

The dataset contains no completely duplicated rows. However, several columns have missing information. The director column has the highest number of missing values, with 2,634 entries. The cast column has 825 missing values, while the country column has 831. The date added column has 10 missing values, the rating column has 4, and the duration column has 3.

During the inspection, I also found three movie records where the running time had been incorrectly placed in the rating column. These records needed correction to ensure that the information was organised properly.

Missing information was handled by identifying unavailable entries rather than treating them as actual values. The date-added column also needed to be converted into a proper date format so that the titles could be analysed according to the year they were added.

Overall, cleaning the dataset was necessary to improve its quality and make the analysis more reliable.

## 4. Content Distribution: Movies and TV Shows

The first part of the analysis focused on comparing the number of Movies and TV Shows in the dataset.

Out of the 8,807 titles, 6,131 are Movies, representing approximately 69.62% of the dataset. The remaining 2,676 are TV Shows, accounting for approximately 30.38%.

This shows that Movies make up the majority of the Netflix titles in the dataset. There are more than twice as many Movies as TV Shows.

This comparison helps us understand the overall composition of the collection and shows that movie content is more heavily represented.

## 5. Analysis of Release Years

The release-year analysis was conducted to understand when the movies and TV shows in the dataset were originally released.

The dataset includes titles released between 1925 and 2021. However, most of the titles were released in more recent years.

The year 2018 has the highest number of titles, with 1,147 records. It is followed by 2017 with 1,032 titles and 2019 with 1,030 titles. The years 2020 and 2016 also have relatively high numbers, with 953 and 902 titles respectively.

The number of titles increases considerably from 2015 onwards, reaches its highest point in 2018 and then gradually decreases.

This suggests that the dataset contains a strong representation of relatively recent content, although older movies and TV shows are also included.

## 6. Analysis of Countries

The country analysis was conducted to identify which countries appear most frequently in the production information.

Some titles were produced by more than one country. Therefore, each country listed for a title was counted separately.

The United States has the highest number of country listings, with 3,689. India follows with 1,046, while the United Kingdom has 804. Canada and France are also among the most frequently listed countries, with 445 and 393 listings respectively.

Japan, Spain, South Korea, Germany and Mexico also appear among the leading countries.

These findings show that the United States has a particularly strong presence in the dataset. However, the collection also includes a wide range of international productions, demonstrating the variety of countries represented.

## 7. Analysis of Genres

The genre analysis was conducted to identify the most common types of content in the dataset.

Each title can belong to more than one genre, so the analysis counts individual genre listings rather than unique titles.

International Movies is the most frequently listed category, with 2,752 listings. Dramas follow with 2,427, while Comedies have 1,674. International TV Shows have 1,351 listings.

Other frequently appearing categories include Documentaries, Action and Adventure, TV Dramas, Independent Movies, Children and Family Movies, and Romantic Movies.

The findings show that the dataset contains a wide variety of entertainment categories. International content, drama and comedy are particularly well represented.

## 8. Analysis of Content Ratings

The rating analysis was conducted to understand the age classifications assigned to the movies and TV shows.

TV-MA is the most frequently recorded rating, with 3,207 titles. TV-14 follows with 2,160 titles. Other common ratings include TV-PG with 863, R with 799 and PG-13 with 490.

The results show that TV-MA and TV-14 are the two most frequently recorded classifications in the dataset.

This provides an understanding of the different audience classifications represented in the collection. However, some ratings are missing or require correction, so these issues should be considered when interpreting the results.

## 9. Analysis of Movie Duration

The movie-duration analysis focused on understanding how long movies in the dataset generally last.

After separating Movies from TV Shows, I examined the recorded running times. There are 6,131 movies with recorded duration information after correcting the three misplaced entries.

The average movie duration is approximately 99.6 minutes, while the median duration is 98 minutes. The most common movie duration is 90 minutes.

The shortest recorded movie lasts 3 minutes, while the longest lasts 312 minutes.

These findings show that most movies in the dataset have a running time of around 90 to 100 minutes, although there are also shorter and considerably longer movies.

## 10. Analysis of TV Show Seasons

Unlike movies, the duration column for TV Shows records the number of seasons rather than the running time.

The analysis shows that 1,793 TV Shows have one season, making it the most common number of seasons. A further 425 shows have two seasons, while 199 have three seasons.

The number of shows generally decreases as the number of seasons increases. The highest recorded number of seasons is 17.

This suggests that TV Shows with only one season are much more common in the dataset than longer-running series.

## 11. Analysis of Netflix Content Additions

The date-added analysis was conducted to understand how many titles were added to Netflix during different years.

The earliest recorded addition date is January 1, 2008, while the latest is September 25, 2021.

The year 2019 has the highest number of recorded additions, with 2,016 titles. In 2020, 1,879 titles were added, followed by 1,498 in 2021. The number of additions also increased considerably between 2016 and 2018.

This shows that the number of titles added to Netflix increased significantly over time, reaching its highest point in 2019 before decreasing in the following years represented in the dataset.

## 12. Overall Findings and Conclusion

The analysis of the Netflix Movies and TV Shows dataset revealed several important patterns.

First, Movies make up approximately 69.62% of the dataset, showing that they are much more common than TV Shows. Most titles were released between 2015 and 2021, with 2018 being the most represented release year.

The country analysis showed that the United States has the highest number of production-country listings, followed by India and the United Kingdom. The genre analysis revealed that International Movies, Dramas and Comedies are the most frequently listed categories.

The rating analysis showed that TV-MA and TV-14 are the most common classifications. The movie-duration analysis found that the average running time is approximately 99.6 minutes, while most TV Shows have only one season.

Finally, the date-added analysis showed that 2019 had the highest number of recorded Netflix additions.

Overall, this project demonstrates how data analysis can be used to understand a large dataset, identify patterns, compare different categories and draw meaningful conclusions from information. It also shows the importance of data cleaning and exploratory data analysis before presenting results.



