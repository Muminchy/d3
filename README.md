#echo 'print("Hello, World!")' > hello.py
import json
import os
from datetime import datetime

# File to store expenses
EXPENSES_FILE = "expenses.json"

def load_expenses():
    """Load expenses from file"""
    if os.path.exists(EXPENSES_FILE):
        with open(EXPENSES_FILE, "r") as f:
            return json.load(f)
    return []

def save_expenses(expenses):
    """Save expenses to file"""
    with open(EXPENSES_FILE, "w") as f:
        json.dump(expenses, f, indent=2)

def add_expense(description, amount, category):
    """Add a new expense"""
    expenses = load_expenses()
    expense = {
        "date": datetime.now().strftime("%Y-%m-%d %H:%M"),
        "description": description,
        "amount": amount,
        "category": category
    }
    expenses.append(expense)
    save_expenses(expenses)
    print(f"✓ Added: {description} - ${amount} ({category})")

def view_expenses():
    """View all expenses"""
    expenses = load_expenses()
    if not expenses:
        print("No expenses yet!")
        return
    
    print("\n--- Your Expenses ---")
    total = 0
    for i, expense in enumerate(expenses, 1):
        print(f"{i}. {expense['date']} | {expense['description']} | ${expense['amount']} | {expense['category']}")
        total += expense['amount']
    print(f"\nTotal: ${total:.2f}\n")

def main():
    """Main menu"""
    while True:
        print("\n=== Expense Tracker ===")
        print("1. Add expense")
        print("2. View expenses")
        print("3. Exit")
        choice = input("Choose (1-3): ")
        
        if choice == "1":
            desc = input("Description: ")
            try:
                amount = float(input("Amount: $"))
                category = input("Category (food/transport/other): ")
                add_expense(desc, amount, category)
            except ValueError:
                print("Invalid amount!")
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            print("Goodbye!")
            break
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
print("yay")
print("why")
srt(98)
