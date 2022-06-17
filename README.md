#include<stdio.h>
#include<string.h>
#include<stdlib.h>

struct items{
char item[20];
float price;
int qty;
};

struct orders{
char customer[50];
char date[50];
int numofItems;
struct items itm[50];
};


void generateBillHeader(char name [50], char date[30]){
printf("\n\n");
printf("\t ADV.RESTAURANT");
printf("\n\t ---------------");
printf("\nDate:%s", date);
printf("\nInvoice To: %s",name);
printf("\n");
printf("---------------------------------------\n");
printf("Items\t\t");
printf("Qty\t\t");
printf("Total \t\t");
printf("\n---------------------------------------");
}
void generateBillBody(char item[30], int qty, float price){
printf("\n%s\t\t",item);
printf("%d\t\t",qty);
printf("%.2f\t",qty * price);
printf("\n");
}
void generateBillFooter(float total){
printf("\n");
float dis = 0.1*total;
float netTotal=total-dis;
float cgst=0.09*netTotal, grandTotal=netTotal + 2*cgst;
printf("---------------------------------------\n");
printf("Sub Total\t\t\t%.2f",total);
printf("\nDiscount @10\t\t\t%.2f", dis);
printf("\n\t\t\t\t-------");
printf("\nNet Total\t\t\t%.2f", netTotal);
printf("\nCGST @9%s\t\t\t%.2f"," ",cgst);
printf("\nSGST @9%s\t\t\t%.2f"," ",cgst);
printf("\n---------------------------------------");
printf("\nGrand Total\t\t\t%.2f",grandTotal);
printf("\n---------------------------------------\n");
}

int main()
{
int opt,n;
float total;
struct orders ord;
// dashboard
printf("\t============ADV. RESTAURANT============");
printf("\n\nPlease select your prefered operation");
printf("\n\n1.Generate Invoice");
printf("\n2. Exit");

printf("\n\nYour choice:\t");

scanf("%d", &opt);
fgetc(stdin);
switch(opt){
    case 1:
    printf("\nPlease enter the name of customer:\t");
    fgets(ord.customer,50,stdin);
    ord.customer[strlen(ord.customer)-1]=0;
    strcpy(ord.date,__DATE__);
    printf("\nPlease enter the number of items:\t");
    scanf("%d",&n);
    printf("\n \n");
    ord.numofItems=n;
    for(int i=0;i<n;i++){
        fgetc(stdin);
        printf("\n\n\nPlease enter the item%d: \t",i+1);
        fgets(ord.itm[i].item,20,stdin);
        ord.itm[i].item[strlen(ord.itm[i].item)-1]=0;
        printf("Please enter the quantity:\t");
        scanf("%d",&ord.itm[i].qty);
        printf("Please enter the unit price:\t");
        scanf("%f",&ord.itm[i].price);
        total += ord.itm[i].qty * ord.itm[i].price;

    }
    generateBillHeader(ord.customer,ord.date);
    for(int i=0;i<ord.numofItems;i++){
        generateBillBody(ord.itm[i].item,ord.itm[i].qty,ord.itm[i].price);}
    generateBillFooter(total); 
    case 2:
    return 0;
}
    return 0;
}
