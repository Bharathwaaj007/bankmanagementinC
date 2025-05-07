#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>
#define max_accounts 100

struct account
{
    int acc_no;
    float balance;
    char name[50];
    int isActive;
};

struct account accounts[max_accounts];
int ac_count=0;

void createnewaccount();
void depositmoney();
void withdrawmoney();
void viewaccstatus();
void deleteaccount();
void displaymenu();
int accountexists(int acc_no);

int main()
{
    int choice;

    while ((1));
    {
        displaymenu();
        printf("please enter your choice from 1 to 6: \n");
        scanf("%d",&choice);
    
    if(choice==1){createnewaccount();}
    else if(choice==2){depositmoney();}
    else if(choice==3){withdrawmoney();}
    else if(choice==4){viewaccstatus();}
    else if(choice==5){deleteaccount();}
    else{printf("no such choice on database....pls try again!");}
    }
    return 0;
}

int accountexists(int acc_no)
{
    for (int i=0;i<ac_count;i++)
    {
        if(accounts[i].acc_no==acc_no && accounts[i].isActive == 1){
            return 1;
        }
    }
    return 0;
}

void createnewaccount()
{
    int acc_no;
    float initial_amount;
    char name[50];

    printf("enter your account number:");
    scanf("%d",&acc_no);

    printf("enter your name.");
    scanf("%s",name);
    
    while (accountexists(acc_no)){
        printf("account number already exists!...enter a new number.");
        }

    printf("enter your initial amount:....must be greater than 1500!");
    scanf("%f",&initial_amount);
    if(initial_amount<1500){
        printf("amount must be greatre than 1500");
    }
    else{
        accounts[ac_count].acc_no = acc_no;
        strcpy(accounts[ac_count].name,name);
        accounts[ac_count].balance=initial_amount;
        ac_count++;
    }

    printf("account created successfully...! \n");
    printf("account number: %d\n",acc_no,"name: %d\n",name,
    "initial balance: %.2f\n",initial_amount);
}

void depositmoney()
{
    int acc_no;
    float deposit;
    
    printf("\n enter your account number:");
    scanf("%d",&acc_no);
    
        if(!accountexists(acc_no)){
            printf("account number does not found. \n");
            return;
        }

        printf("\n enter your deposit money:");
        scanf("%f",&deposit);

        for (int i=0;i<ac_count;i++){
            if(accounts[i].acc_no==acc_no){
                accounts[i].balance+=deposit;
                printf("deposit successful.....");
                printf("your account name: %d\n",acc_no,"balance money: %f\n",accounts[i].balance);
                return;
                }
            }
}

void withdrawmoney()
{
    int acc_no;
    float money;
    int found=0;

    printf("enter your account number: \n");
    scanf("%d",&acc_no);

    if(accountexists(acc_no)){
        

        for (int i=0;i<ac_count;i++){
           if(accounts[i].acc_no==acc_no){
             found=1;
             printf("enter withdrawl amount: \n");
             scanf("%f",&money);
             
             if(money<=accounts[i].balance){
                accounts[i].balance-=money;
                printf("withdrawl successful. \n");
                printf("your balance is: %f\n",accounts[i].balance);
            }
            else{
                printf("no sufficient blance in the account!");
                break;
            }
            break;
           }
        }

        if(!found){
            printf("account does not exist. \n");
        }
    }
}

void viewaccstatus()
{
    int acc_no,f=0;

    printf("enter your account number:");
    scanf("%d",&acc_no);

    for(int i=0;i<ac_count;i++)
    {
        if(accounts[i].acc_no==acc_no){
            f=1;
            printf("\n -----------ACCOUNT STATUS------------ \n");
            printf("account number: %d\n",accounts[i].acc_no);
            printf("account holder name: %s\n",accounts[i].name);
            printf("current balance: %.3f\n",accounts[i].balance);
            printf("\n --------------------------------------- \n");

            break;
        }
    }

    if(!f){
        printf("\n account not found plesae try again. \n");
    }
}

void deleteaccount()
{
    int acc_no,found=0;

    printf("enter your account number:");
    scanf("%d",&acc_no);

    for(int i=0;i<ac_count;i++){
        if(accounts[i].acc_no==acc_no && accounts[i].isActive==1)
        {
            accounts[i].isActive=0;
            printf(" \n account deleted successfully. \n");
            return;
        }
        else{
            printf("\n account number does not exists. \n");
            break;
        }
    }
    printf("\n account number not found. \n");
}

void displaymenu()
{
    printf("\n ~~~~~~~~~~~~~~~welcome to bank's portal~~~~~~~~~~~~~~~~~~~");
    printf("\n please enter your choice from 1 to 6.....");
    printf(" \n press 1 for creating new account.");
    printf(" \n press 2 for deposit money.");
    printf("\n press 3 to view your current account status.\n");
    printf("\n press 5 to delete your accpunt.");
    printf("\n ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
}

