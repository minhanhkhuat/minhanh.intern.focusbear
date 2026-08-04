# Learning Python Programming Concepts

## Tasks
```python
#task 1
print("Hello, My name is Minh Anh")
#task 2
num1 = float(input("Enter the first number: "))
num2 = float(input("Enter the second number: "))
print(f"Sum: {num1 + num2}")
print(f"Difference: {num1 - num2}")
print(f"Product: {num1 * num2}")
print(f"Quotient: {num1 / num2 if num2 != 0 else 'Error (Division by zero)'}")

# Task 3: User input and age calculation
human_age = float(input("Enter your age in human years: "))
dog_years = human_age * 7

print(f"You are approximately {dog_years:.1f} years old in dog years!")

# Task 4: Strings and creative formatting
favourite_food = input("What is your favourite food? ")
print(f"Legend has it that eating {favourite_food.title()} grants +100 coding power and instant productivity!")

# Task 5: Random numbers and conditional statements
import random

target_number = random.randint(1, 10)
user_guess = int(input("Guess a number between 1 and 10: "))

if user_guess == target_number:
    print(" Incredible! You guessed the exact number!")
elif user_guess > target_number:
    print(f"Too high! The secret number was {target_number}.")
else:
    print(f"Too low! The secret number was {target_number}.")
```
## Reflection
1. Which task did you find the most fun?
The Number Guessing Game was the most enjoyable task because it introduced interactivity and state logic. Bringing together dynamic user inputs, conditional checking (`if/elif/else`), and the `random` module transformed static code into an interactive experience.

2. How did you feel when you saw your code running correctly for the first time?
Seeing the terminal return the exact expected output without throwing syntax or execution errors was immensely satisfying. It reinforces the feedback loop of programming: breaking down a problem into logical steps, implementing the solution, and seeing immediate functional results.

3. How could you imagine using these skills to solve problems or make daily tasks easier?
- Automating Repetitive Tasks: Using basic loops and conditional statements to rename bulk files, clean up structured text documents, or move files automatically into organized folders.
- Streamlining Calculations: Creating lightweight CLI scripts to perform quick math calculations, conversions, or data transformations without needing heavy spreadsheet software.
- Building Utility Tools: Developing habit-tracking utilities or automated micro-break notifications similar to features in Focus Bear to boost personal focus and daily productivity.