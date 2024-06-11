# pennywisetracker
import csv
import os

# File to store expenses
expense_file = 'expenses.csv'

# Function to initialize the CSV file
def initialize_file():
    if not os.path.exists(expense_file):
        with open(expense_file, mode='w', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(["Date", "Category", "Description", "Amount"])

# Function to add a new expense
def add_expense(date, category, description, amount):
    with open(expense_file, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([date, category, description, amount])

# Function to view all expenses
def view_expenses():
    with open(expense_file, mode='r') as file:
        reader = csv.reader(file)
        next(reader)  # Skip header
        for row in reader:
            print(f"Date: {row[0]}, Category: {row[1]}, Description: {row[2]}, Amount: {row[3]}")

# Function to categorize expenses
def view_expenses_by_category(category):
    with open(expense_file, mode='r') as file:
        reader = csv.reader(file)
        next(reader)  # Skip header
        for row in reader:
            if row[1] == category:
                print(f"Date: {row[0]}, Category: {row[1]}, Description: {row[2]}, Amount: {row[3]}")

def main():
    initialize_file()

    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. View Expenses by Category")
        print("4. Exit")
        choice = input("Choose an option: ")

        if choice == '1':
            date = input("Enter date (YYYY-MM-DD): ")
            category = input("Enter category: ")
            description = input("Enter description: ")
            amount = input("Enter amount: ")
            add_expense(date, category, description, amount)
            print("Expense added successfully!")
        elif choice == '2':
            print("Expenses:")
            view_expenses()
        elif choice == '3':
            category = input("Enter category: ")
            print(f"Expenses in category '{category}':")
            view_expenses_by_category(category)
        elif choice == '4':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
