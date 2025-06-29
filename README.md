import csv
import os

# File to store transactions
FILE_NAME = "transactions.csv"

# Create the CSV file if it doesn't exist
if not os.path.exists(FILE_NAME):
    with open(FILE_NAME, mode='w', newline='') as file:
        writer = csv.writer(file)
        writer.writerow(["Type", "Description", "Amount"])

def add_transaction(t_type, description, amount):
    with open(FILE_NAME, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([t_type, description, amount])
    print("Transaction added successfully.")

def show_summary():
    total_income = 0
    total_expense = 0

    with open(FILE_NAME, mode='r') as file:
        reader = csv.DictReader(file)
        for row in reader:
            amount = float(row['Amount'])
            if row['Type'] == 'Income':
                total_income += amount
            elif row['Type'] == 'Expense':
                total_expense += amount

    balance = total_income - total_expense
    print("\n--- Summary ---")
    print(f"Total Income : {total_income}")
    print(f"Total Expense: {total_expense}")
    print(f"Balance      : {balance}\n")

def show_transactions():
    print("\n--- Transaction History ---")
    with open(FILE_NAME, mode='r') as file:
        reader = csv.reader(file)
        for row in reader:
            print("\t".join(row))
    print()

# Main Menu
while True:
    print("==== Simple Accounting App ====")
    print("1. Add Income")
    print("2. Add Expense")
    print("3. View Summary")
    print("4. View All Transactions")
    print("5. Exit")

    choice = input("Enter your choice (1-5): ")

    if choice == '1':
        desc = input("Enter income description: ")
        amt = float(input("Enter amount: "))
        add_transaction("Income", desc, amt)
    elif choice == '2':
        desc = input("Enter expense description: ")
        amt = float(input("Enter amount: "))
        add_transaction("Expense", desc, amt)
    elif choice == '3':
        show_summary()
    elif choice == '4':
        show_transactions()
    elif choice == '5':
        print("Exiting program.")
        break
    else:
        print("Invalid choice. Try again.")
