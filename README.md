# Python-assignement-7
OOPs banking
# Bank system simulation
class BankAccount:
    def __init__(self, account_number, pin, balance=0):
        self.account_number = account_number
        self.pin = pin
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposited ${amount}. Current balance: ${self.balance}")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if amount > 0 and amount <= self.balance:
            self.balance -= amount
            print(f"Withdrew ${amount}. Current balance: ${self.balance}")
        elif amount > self.balance:
            print("Insufficient funds!")
        else:
            print("Invalid withdrawal amount.")

    def check_balance(self):
        print(f"Current balance: ${self.balance}")

# Bank system functions
class BankingSystem:
    def __init__(self):
        # For simplicity, creating one sample account
        self.accounts = {
            "12345": BankAccount("12345", "1234", 1000)  # Sample account: account_number, pin, balance
        }
        self.logged_in_account = None

    def login(self, account_number, pin):
        if account_number in self.accounts and self.accounts[account_number].pin == pin:
            self.logged_in_account = self.accounts[account_number]
            print(f"Login successful. Welcome, Account #{account_number}!")
        else:
            print("Invalid account number or pin.")

    def logout(self):
        if self.logged_in_account:
            print(f"Logged out from Account #{self.logged_in_account.account_number}.")
            self.logged_in_account = None
        else:
            print("No account is logged in.")

    def run(self):
        while True:
            print("\n--- Banking System ---")
            if not self.logged_in_account:
                print("1. Login")
            else:
                print("1. Deposit Money")
                print("2. Withdraw Money")
                print("3. Check Balance")
                print("4. Logout")

            print("5. Exit")

            choice = input("Choose an option: ")

            if choice == "1":
                if self.logged_in_account:
                    amount = float(input("Enter deposit amount: $"))
                    self.logged_in_account.deposit(amount)
                else:
                    account_number = input("Enter account number: ")
                    pin = input("Enter pin: ")
                    self.login(account_number, pin)

            elif choice == "2":
                if self.logged_in_account:
                    amount = float(input("Enter withdrawal amount: $"))
                    self.logged_in_account.withdraw(amount)
                else:
                    print("Please log in first.")

            elif choice == "3":
                if self.logged_in_account:
                    self.logged_in_account.check_balance()
                else:
                    print("Please log in first.")

            elif choice == "4":
                if self.logged_in_account:
                    self.logout()
                else:
                    print("No account logged in.")

            elif choice == "5":
                print("Thank you for using the banking system. Goodbye!")
                break

            else:
                print("Invalid option. Please try again.")

# Run the banking system
bank_system = BankingSystem()
bank_system.run()
