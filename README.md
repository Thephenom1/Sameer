# Sameer
Bank.management system
#include <stdio.h>

#include <stdlib.h>

#include <string.h>

// Structure to represent a bank account

typedef struct Account {

    int accountNumber;

    char accountHolder[100];

    float balance;

    struct Account* next;

} Account;

Account* head = NULL;

// Function prototypes

void displayMenu();

void createAccount();

void displayAllAccounts();

void displayAccountDetails(int accountNumber);

void deposit(int accountNumber, float amount);

void withdraw(int accountNumber, float amount);

void deleteAccount(int accountNumber);

// Function to display the menu

void displayMenu() {

    printf("\nBank Management System\n");

    printf("1. Create Account\n");

    printf("2. Display All Accounts\n");

    printf("3. Display Account Details\n");

    printf("4. Deposit Amount\n");

    printf("5. Withdraw Amount\n");

    printf("6. Delete Account\n");

    printf("7. Exit\n");

}

// Function to create a new account

void createAccount() {

    Account* newAccount = (Account*)malloc(sizeof(Account));

    printf("Enter Account Number: ");

    scanf("%d", &newAccount->accountNumber);

    getchar();  // Clearing the input buffer

    printf("Enter Account Holder Name: ");

    fgets(newAccount->accountHolder, 100, stdin);

    newAccount->accountHolder[strcspn(newAccount->accountHolder, "\n")] = '\0';  // Removing newline character

    printf("Enter Initial Balance: ");

    scanf("%f", &newAccount->balance);

    newAccount->next = NULL;

    // Insert the new account at the beginning of the linked list

    if (head == NULL) {

        head = newAccount;

    } else {

        newAccount->next = head;

        head = newAccount;

    }

    printf("Account created successfully!\n");

}

// Function to display details of all accounts

void displayAllAccounts() {

    if (head == NULL) {

        printf("No accounts found!\n");

        return;

    }

    Account* current = head;

    printf("\nAccount Details\n");

    printf("-------------------------------------------------\n");

    printf("Account Number\tAccount Holder\tBalance\n");

    printf("-------------------------------------------------\n");

    while (current != NULL) {

        printf("%d\t\t%s\t\t%.2f\n", current->accountNumber, current->accountHolder, current->balance);

        current = current->next;

    }

    printf("-------------------------------------------------\n");

}

// Function to display details of a specific account

void displayAccountDetails(int accountNumber) {

    if (head == NULL) {

        printf("No accounts found!\n");

        return;

    }

    Account* current = head;

    while (current != NULL) {

        if (current->accountNumber == accountNumber) {

            printf("\nAccount Details\n");

            printf("-------------------------------------------------\n");

            printf("Account Number\tAccount Holder\tBalance\n");

            printf("-------------------------------------------------\n");

            printf("%d\t\t%s\t\t%.2f\n", current->accountNumber, current->accountHolder, current->balance);

            printf("-------------------------------------------------\n");

            return;

        }

        current = current->next;

    }

    printf("Account not found!\n");

}

// Function to deposit amount into an account

void deposit(int accountNumber, float amount) {

    if (head == NULL) {

        

                   printf("No accounts found!\n");

        return;

    }

    Account* current = head;

    while (current != NULL) {

        if (current->accountNumber == accountNumber) {

            current->balance += amount;

            printf("Amount deposited successfully!\n");

            printf("Updated Balance: %.2f\n", current->balance);

            return;

        }

        current = current->next;

    }

    printf("Account not found!\n");

}

// Function to withdraw amount from an account

void withdraw(int accountNumber, float amount) {

    if (head == NULL) {

        printf("No accounts found!\n");

        return;

    }

    Account* current = head;

    while (current != NULL) {

        if (current->accountNumber == accountNumber) {

            if (current->balance >= amount) {

                current->balance -= amount;

                printf("Amount withdrawn successfully!\n");

                printf("Updated Balance: %.2f\n", current->balance);

            } else {

                printf("Insufficient balance!\n");

            }

            return;

        }

        current = current->next;

    }

    printf("Account not found!\n");

}

// Function to delete an account

void deleteAccount(int accountNumber) {

    if (head == NULL) {

        printf("No accounts found!\n");

        return;

    }

    if (head->accountNumber == accountNumber) {

        Account* temp = head;

        head = head->next;

        free(temp);

        printf("Account deleted successfully!\n");

        return;

    }

    Account* current = head;

    Account* previous = NULL;

    while (current != NULL) {

        if (current->accountNumber == accountNumber) {

            previous->next = current->next;

            free(current);

            printf("Account deleted successfully!\n");

            return;

        }

        previous = current;

        current = current->next;

    }

    printf("Account not found!\n");

}

int main() {

    int choice;

    int accountNumber;

    float amount;

    while (1) {

        displayMenu();

        printf("Enter your choice: ");

        scanf("%d", &choice);

        switch (choice) {

            case 1:

                createAccount();

                break;

            case 2:

                displayAllAccounts();

                break;

            case 3:

                printf("Enter Account Number: ");

                scanf("%d", &accountNumber);

                displayAccountDetails(accountNumber);

                break;

            case 4:

                printf("Enter Account Number: ");

                scanf("%d", &accountNumber);

                printf("Enter Amount to Deposit: ");

                scanf("%f", &amount);

                deposit(accountNumber, amount);

                break;

            case 5:

                printf("Enter Account Number: ");

                scanf("%d", &accountNumber);

                printf("Enter Amount to Withdraw: ");

                scanf("%f", &amount);

                withdraw(accountNumber, amount);

                break;

            case 6:

                printf("Enter Account Number: ");

                scanf("%d", &accountNumber);

                deleteAccount(accountNumber);

                break;

            case 7:

                printf("Exiting... Thank you!\n");

                exit(0);

            default:

                printf("Invalid choice! Please try again.\n");

                break;

        }

    }

    return 0;

}
