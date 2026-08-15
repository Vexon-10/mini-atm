# mini-atm
"""Day 1 of 100 Days of Python: Mini ATM System."""

account = {
    "name": "MalwareMint",
    "balance": 50_000,
    "pin": "1234",
    "type": "Business Account",
}


def get_amount(prompt):
    """Keep asking until the user enters a positive whole-number amount."""
    while True:
        try:
            amount = int(input(prompt))
            if amount <= 0:
                print("Please enter an amount greater than zero.")
                continue
            return amount
        except ValueError:
            print("Invalid amount. Please enter a whole number.")


def show_balance():
    print(f"Your balance is: ₹{account['balance']:,}")


def show_account_details():
    print("\n--- Account Details ---")
    print(f"Account name: {account['name']}")
    print(f"Account balance: ₹{account['balance']:,}")
    print(f"Account type: {account['type']}")


print("=== MINI ATM ===")
pin = input("Enter your PIN: ").strip()

if pin != account["pin"]:
    print("Invalid PIN. Access denied.")
else:
    print(f"Welcome, {account['name']}!")

    while True:
        print("\n**** ATM MENU ****")
        print("1. Check balance")
        print("2. Deposit money")
        print("3. Withdraw money")
        print("4. Account details")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ").strip()

        if choice == "1":
            show_balance()

        elif choice == "2":
            amount = get_amount("Enter deposit amount: ₹")
            account["balance"] += amount
            print("Money deposited successfully.")
            show_balance()

        elif choice == "3":
            amount = get_amount("Enter withdrawal amount: ₹")

            if amount > account["balance"]:
                print("Insufficient balance.")
            else:
                account["balance"] -= amount
                print("Please collect your cash.")
                show_balance()

        elif choice == "4":
            show_account_details()

        elif choice == "5":
            print("Thank you for using our ATM. Goodbye!")
            break

        else:
            print("Invalid choice. Please enter a number from 1 to 5.")
