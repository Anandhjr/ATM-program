// # ATM-program
// this is basic ATM program, that allows , pin and user authentication , amount updating after withdrawal these kind things ( NOTE : I'm a beginner ) 

import time
import winsound

# documentation this code
"""
Title: SBI ATM Program

Description:
Simulates an ATM for SBI Bank. Allows card insertion, PIN authentication, withdrawals, and balance checks.

Features:
- User authentication via username and PIN.
- Withdrawal with balance update.
- Basic error handling.
- Sound effects.

Variables:
- users: List of registered usernames.
- users_card: Dictionary mapping card PINs to usernames.
- anandh_amount, deepa_amount: Initial account balances.
- card_set: Status of card insertion.
- turns: Counter for failed username attempts.
- pin_number: Entered PIN.
- amount: Withdrawal amount.
- balance_1: User's response for balance check.

Usage:
1. Run the script.
2. Follow prompts for card insertion, username, PIN, withdrawal, and balance check.

Notes:
- Simplified simulation, not real banking.
- Basic error handling, no encryption for PINs.
"""

time.sleep(2)
print("  Welcome to SBI ATM! ")
winsound.PlaySound('GREETINGS ATM.wav', winsound.SND_FILENAME)

# Variable initialization like users_name , user_amount , atm_balance , user_card_details
card = False
available_money = 50000

users = ['anandh', 'deepa']
users_card = {
    "7094": "anandh",
    "9999": "deepa"
}
anandh_amount = 25000
deepa_amount = 7000

time.sleep(1)

# Card insertion prompt
card_set = input("Please insert your card: ")
print("Please wait....")
time.sleep(5)

# Validate card insertion
while card_set.lower() != "inserted":
    print("Please enter 'inserted' to insert your card.")
    card_set = input("Please insert your card: ")
card = True

# Username authentication checking loop
turns = 0
while True:
    name = input("Enter your name: ")
    if name in users:
        print("Welcome, ", name, "!")
        break
    else:
        turns += 1
        print("ERROR!")
        print("Your username was incorrect!")
        if turns >= 3:
            print("You have entered an incorrect username multiple times. Please try again later.")
            exit()  # Exit the program after multiple failed attempts

# PIN authentication
pin_number = input("Enter your 4-digit pin number: ")
while len(pin_number) != 4:
    print("ERROR!")
    print("Pin numbers contain only four digits!")
    pin_number = input("Enter your 4-digit pin number: ")

while pin_number not in users_card:
    print("You entered a wrong pin number!")
    pin_number = input("Enter your pin number: ")

# Withdrawal
amount = int(input("Enter an amount: "))
while amount > 100000:
    print("Amount cannot be greater than 10,000.")
    amount = int(input("Enter an amount below 10,000: "))

if pin_number == "7094":
    anandh_amount -= amount  # Update Anandh's amount after withdrawal
    while amount > anandh_amount:
        print(f"You only have {anandh_amount} in your bank account.")
        amount = int(input(f"Enter an amount below {anandh_amount}: "))
elif pin_number == "9999":
    deepa_amount -= amount  # Update Deepa's amount after withdrawal
    while amount > deepa_amount:
        print(f"You only have {deepa_amount} in your bank account.")
        amount = int(input(f"Enter an amount below {deepa_amount}: "))

# Transaction sound effects
winsound.PlaySound('ATM.wav', winsound.SND_FILENAME)
print("Collect your cash!")
winsound.Beep(800, 60*20)
winsound.Beep(800, 60*20)
winsound.Beep(800, 60*20)
time.sleep(2)

# Balance check
balance_1 = input("Do you want to know the balance amount details? (1 for yes / 2 for no)")
if balance_1 == 1:
     if pin_number == "7094":
         print(f"Balance amount: {anandh_amount}")
     elif pin_number == "9999":
         print(f"Balance amount: {deepa_amount}")
         time.sleep(2)
         print("-" * 20)
         print("Thank you for using SBI ATM!")
         exit()
else:
     time.sleep(2)
     print("-" * 20)
     print("Thank you for using SBI ATM!")
