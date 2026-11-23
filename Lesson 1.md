
# DATA ANALYSIS LEARNING
# LESSON 1: PYTHON BASICS


# 1. VARIABLES AND DATA TYPES

print("1. Variables are used to store information.")

name = "Sonam"
age = 17
height = 1.65
is_learning = True

print("Name:", name)
print("Age:", age)
print("Height:", height)
print("Learning Data Analysis:", is_learning)

# Check data types
print(type(name))
print(type(age))
print(type(height))
print(type(is_learning))

# 2. LISTS

print("\n3. LISTS")
print("A list stores multiple values in one variable.")

movies = ["Avatar", "Titanic", "Inception", "Interstellar"]

print("All movies:", movies)
print("First movie:", movies[0])
print("Last movie:", movies[-1])

# Add a movie
movies.append("The Batman")

# Remove a movie
movies.remove("Titanic")

print("Updated movie list:", movies)
print("Number of movies:", len(movies))


# 3. TUPLES

print("\n4. TUPLES")
print("Tuples are similar to lists, but their values cannot be changed after creation.")
release_years = (2009, 1997, 2010, 2014)

print("Release years:", release_years)
print("First year:", release_years[0])
print("Total years:", len(release_years))


# 4. DICTIONARIES

print("\n5. DICTIONARIES")

movie = {
    "title": "Inception",
    "year": 2010,
    "rating": 8.8,
    "genre": "Science Fiction"
}

print("Movie information:", movie)

print("Title:", movie["title"])
print("Year:", movie["year"])
print("Rating:", movie["rating"])

# Add a new value
movie["director"] = "Christopher Nolan"

print("Updated dictionary:", movie)


# 5. CONDITIONAL STATEMENTS

print("\n6. CONDITIONAL STATEMENTS")

rating = 8.5

if rating >= 8:
    print("Highly rated")

elif rating >= 5:
    print("Average rated")

else:
    print("Low rated")


# 6. FOR LOOPS

print("\n7. FOR LOOPS")

movies = ["Avatar", "Titanic", "Inception"]

for movie in movies:
    print(movie)


# 7. WHILE LOOPS

print("\n8. WHILE LOOPS")

number = 1

while number <= 5:
    print(number)
    number += 1


# 8. FUNCTIONS

print("\n9. FUNCTIONS")

def calculate_average(numbers):
    average = sum(numbers) / len(numbers)
    return average

ratings = [8, 9, 7, 10, 6]

result = calculate_average(ratings)

print("Average rating:", result)


# 9. BASIC DATA ANALYSIS PRACTICE

print("\n10. BASIC DATA ANALYSIS")

# Sample movie data
movie_names = ["Avatar", "Titanic", "Inception", "Interstellar"]
movie_ratings = [7.9, 7.9, 8.8, 8.6]

# Calculate average rating
average_rating = sum(movie_ratings) / len(movie_ratings)

# Find highest and lowest ratings
highest_rating = max(movie_ratings)
lowest_rating = min(movie_ratings)

print("Total movies:", len(movie_names))
print("Average rating:", average_rating)
print("Highest rating:", highest_rating)
print("Lowest rating:", lowest_rating)

# Display movies and their ratings
for i in range(len(movie_names)):
    print(movie_names[i], ":", movie_ratings[i])


# ==========================================
# END OF LESSON 1
# ==========================================

print("\nLesson 1 completed!")


