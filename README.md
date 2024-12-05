# PLS-Assignment-Using-C-Programming



#include <stdio.h>
#include <stdlib.h>

#define MAX_ATTEMPTS 3

void checkBalance(double balance);
void deposit(double *balance);
void withdraw(double *balance);

int main() {
    double balance = 0.0;
    int choice;
    int pin = 1234;
    int enteredPin;
    int attempts = 0;

    // PIN Verification with attempts limit
    while (attempts < MAX_ATTEMPTS) {
        printf("Enter your PIN: ");
        scanf("%d", &enteredPin);

        if (enteredPin == pin) {
            printf("Access Granted.\n");
            break;
        } else {
            attempts++;
            printf("Incorrect PIN. %d attempts remaining.\n", MAX_ATTEMPTS - attempts);
        }

        if (attempts == MAX_ATTEMPTS) {
            printf("Maximum attempts exceeded. Access Denied.\n");
            return 0;
        }
    }

    // ATM Menu
    do {
        printf("\n*** ATM Menu ***\n");
        printf("1. Check Balance\n");
        printf("2. Deposit Money\n");
        printf("3. Withdraw Money\n");
        printf("4. Exit\n");
        printf("Please select an option (1-4): ");
        
        if (scanf("%d", &choice) != 1) {
            printf("Invalid input. Please enter a number.\n");
            while (getchar() != '\n'); // Clear the input buffer
            continue;
        }

        switch (choice) {
            case 1:
                checkBalance(balance);
                break;
            case 2:
                deposit(&balance);
                break;
            case 3:
                withdraw(&balance);
                break;
            case 4:
                printf("Thank you for using the ATM. Goodbye!\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 4);

    return 0;
}

// Function to check account balance
void checkBalance(double balance) {
    printf("Your current balance is: $%.2lf\n", balance);
}

// Function to deposit money
void deposit(double *balance) {
    double amount;
    printf("Enter amount to deposit: $");
    if (scanf("%lf", &amount) != 1 || amount <= 0) {
        printf("Invalid deposit amount. Please enter a positive number.\n");
        while (getchar() != '\n'); // Clear the input buffer
        return;
    }
    *balance += amount;
    printf("Deposited $%.2lf. Your new balance is: $%.2lf\n", amount, *balance);
}

// Function to withdraw money
void withdraw(double *balance) {
    double amount;
    printf("Enter amount to withdraw: $");
    if (scanf("%lf", &amount) != 1 || amount <= 0) {
        printf("Invalid withdrawal amount. Please enter a positive number.\n");
        while (getchar() != '\n'); // Clear the input buffer
        return;
    }
    if (amount > *balance) {
        printf("Insufficient funds. Your balance is: $%.2lf\n", *balance);
    } else {
        *balance -= amount;
        printf("Withdrew $%.2lf. Your new balance is: $%.2lf\n", amount, *balance);
    }
}
