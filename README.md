#include <stdio.h>

int main() {
    int has, acc, choice, pin;
    long long num;
    float bal = 50000.0, a, b;
    int otp, ver = 0;

    printf("Do you have a card? (1 for Yes / 0 for No): ");
    scanf("%d", &has);

    if (has == 0) {
        printf("Please enter your 16-digit account number: ");
        scanf("%lld", &num);
        if (num >= 1000000000000000LL && num <= 9999999999999999LL) {
            printf("otp has been sent to your registered mobile number\n");
        } else {
            printf("Invalid number. It must be exactly 16 digits.\n");
            printf("Enter your 16-digit account number again: ");
            scanf("%lld", &num);
            if (num >= 1000000000000000LL && num <= 9999999999999999LL) {
                printf("otp has been sent to your registered mobile number\n");
            } else {
                printf("Invalid number. It must be exactly 16 digits.\n");
                printf("Enter your 16-digit account number again: ");
                scanf("%lld", &num);
                if (num >= 1000000000000000LL && num <= 9999999999999999LL) {
                    printf("An OTP has been sent to your registered mobile number.\n");
                } else {
                    printf("Maximum attempts reached. Exiting...\n");
                    return 0;
                }
            }
        }
        printf("Enter 6 digit OTP: ");
        scanf("%d", &otp);
        if (otp >= 100000 && otp <= 999999) {
            ver = 1;
        } else {
            printf("Invalid OTP. Please try again.\n");
            printf("Enter 6-digit OTP: ");
            scanf("%d", &otp);
            if (otp >= 100000 && otp <= 999999) {
                ver = 1;
            } else {
                printf("Invalid OTP. Please try again.\n");
                printf("Enter 6-digit OTP: ");
                scanf("%d", &otp);
                if (otp >= 100000 && otp <= 999999) {
                    ver = 1;
                } else {
                    printf("Maximum OTP attempts reached. Exiting...\n");
                    return 0;
                }
            }
        }
    } else if (has == 1) {
        printf("Please insert your card.");
        char ch;
        scanf("%c%c", &ch, &ch);
        printf("Card inserted successfully.\n");
    } else {
        printf("Invalid input. Please restart and select 1 or 0 only.\n");
        return 0;
    }

    if (has == 1 || ver == 1) {
        printf("\nWelcome to the ATM.\n");
        printf("Select account type:\n");
        printf("1. Savings\n2. Current\n");
        printf("Enter your choice: ");
        scanf("%d", &acc);

        if (acc == 1 || acc == 2) {
            printf("\nATM Menu:\n");
            printf("1. Balance Inquiry\n");
            printf("2. Withdraw Cash\n");
            printf("3. Deposit Money\n");
            printf("4. Exit\n");
            printf("Enter your choice: ");
            scanf("%d", &choice);

            if (choice == 1) {
                printf("Enter your 4-digit PIN: ");
                scanf("%d", &pin);
                if (pin >= 1000 && pin <= 9999) {
                    printf("Your current balance is ₹%g\n", bal);
                } else {
                    printf("Invalid PIN.\n");
                }
            } else if (choice == 2) {
                printf("Enter amount to withdraw: ₹");
                scanf("%f", &a);
                if (a <= 0) {
                    printf("Invalid amount.\n");
                } else {
                    printf("Enter your 4-digit PIN: ");
                    scanf("%d", &pin);
                    if (pin >= 1000 && pin <= 9999) {
                        if (a > 20000)
                            printf("Maximum withdrawal limit is ₹20,000.\n");
                        else if (a > bal)
                            printf("Insufficient balance.\n");
                        else if (acc == 2 && (bal - a) < 5000)
                            printf("Maintain min ₹5,000 in Current account.\n");
                        else if ((int)a % 100 != 0)
                            printf("Enter amount in ₹100/₹200/₹500.\n");
                        else {
                            bal -= a;
                            printf("Collect your cash: ₹%g\n", a);
                            printf("Remaining balance: ₹%g\n", bal);
                        }
                    } else {
                        printf("Invalid PIN.\n");
                    }
                }
            } else if (choice == 3) {
                printf("Enter amount to deposit: ₹");
                scanf("%f", &b);
                if (b <= 0) {
                    printf("Invalid amount.\n");
                } else {
                    printf("Enter your 4-digit PIN: ");
                    scanf("%d", &pin);
                    if (pin >= 1000 && pin <= 9999) {
                        if (b > 200000)
                            printf("Max deposit ₹2,00,000.\n");
                        else if ((int)b % 100 != 0)
                            printf("Deposits in ₹100/₹200/₹500 notes.\n");
                        else {
                            bal += b;
                            printf("₹%g deposited successfully.\n", b);
                            printf("Updated balance: ₹%g\n", bal);
                        }
                    } else {
                        printf("Invalid pin.\n");
                    }
                }
            } else if (choice == 4) {
                printf("Thank you. Collect your card.\n");
            } else {
                printf("Invalid option.\n");
            }
        } else {
            printf("Invalid account type.\n");
        }
    } else {
        printf("Authentication failed. Exiting...\n");
    }

    return 0;
}
