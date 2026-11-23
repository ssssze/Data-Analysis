# DATA ANALYSIS LEARNING
# LESSON 1: PYTHON BASICS

# 1. VARIABLES

print("----- VARIABLES -----")

name = "Sonam"
age = 17
subject = "Data Analysis"

print("Name:", name)
print("Age:", age)
print("Subject:", subject)


# 2. DATA TYPES

print("\n----- DATA TYPES -----")

name = "Python"       # String
number = 25           # Integer
price = 15.5          # Float
is_learning = True    # Boolean

print(type(name))
print(type(number))
print(type(price))
print(type(is_learning))


# 3. MATHEMATICAL OPERATORS

print("\n----- MATHEMATICAL OPERATORS -----")

a = 20
b = 10

print("Addition:", a + b)
print("Subtraction:", a - b)
print("Multiplication:", a * b)
print("Division:", a / b)
print("Floor Division:", a // b)
print("Power:", a ** b)
print("Remainder:", a % b)


# 4. LISTS

print("\n----- LISTS -----")

numbers = [10, 20, 30, 40, 50]

print("List:", numbers)
print("First element:", numbers[0])
print("Last element:", numbers[-1])

# Adding an element
numbers.append(60)

# Removing an element
numbers.remove(20)

print("Updated list:", numbers)
print("Number of elements:", len(numbers))


# 5. TUPLES

print("\n----- TUPLES -----")

years = (2020, 2021, 2022, 2023, 2024)

print("Years:", years)
print("First year:", years[0])
print("Total years:", len(years))


# 6. DICTIONARIES

print("\n----- DICTIONARIES -----")

student = {
    "name": "Alex",
    "age": 17,
    "grade": 11,
    "subject": "Mathematics"
}

print("Student information:", student)

# Accessing values
print("Name:", student["name"])
print("Grade:", student["grade"])

# Adding a new item
student["school"] = "Royal Academy"

print("Updated dictionary:", student)


# 7. CONDITIONAL STATEMENTS

print("\n----- CONDITIONAL STATEMENTS -----")

marks = 75

if marks >= 80:
    print("Grade: A")

elif marks >= 60:
    print("Grade: B")

elif marks >= 40:
    print("Grade: C")

else:
    print("Grade: Fail")


# 8. FOR LOOPS

print("\n----- FOR LOOPS -----")

numbers = [1, 2, 3, 4, 5]

for number in numbers:
    print(number)


# 9. WHILE LOOPS

print("\n----- WHILE LOOPS -----")

count = 1

while count <= 5:
    print(count)
    count += 1


# 10. FUNCTIONS

print("\n----- FUNCTIONS -----")

def calculate_average(numbers):

    total = sum(numbers)
    average = total / len(numbers)

    return average


marks = [70, 85, 90, 65, 80]

result = calculate_average(marks)

print("Average marks:", result)


# 11. BUILT-IN FUNCTIONS

print("\n----- BUILT-IN FUNCTIONS -----")

numbers = [15, 30, 45, 60, 75]

print("Total:", sum(numbers))
print("Maximum:", max(numbers))
print("Minimum:", min(numbers))
print("Length:", len(numbers))
print("Sorted:", sorted(numbers))


# 12. STRING OPERATIONS

print("\n----- STRING OPERATIONS -----")

text = "learning python"

print("Original:", text)
print("Uppercase:", text.upper())
print("Lowercase:", text.lower())
print("Capitalized:", text.capitalize())
print("Length:", len(text))


# ==========================================
# END OF LESSON 1
# ==========================================

print("\nLesson 1 completed successfully!")

