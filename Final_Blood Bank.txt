#include<stdio.h>
#include<windows.h>
#include<conio.h>
#include<string.h>
#include<time.h>

#define speed 3

void admin_mainmenu(void);
void firstPage();
void login(int);
void admin_design();
void newdonor();
void viewdonor();
void deletedonor();
void searchdonor();
void guest_mainmenu();
void guest_design();
void contact();
void print_admin();
void print_load_slow();
int getdata();
void print_guest();
void donorlist();
void print_slow(char per[1000]);
void date();
int  checkid(int);


char password[10] = "1";

char catagories[][25]={"A+", "A-", "B+", "B-", "AB+", "AB-", "O+", "O-"};

struct blood{
    char name[30];
    char address[20];
    char email[20];
    int phone;
    int donor_id;
    char *cat;
    char *sr;
};

struct blood donor;
FILE *fp, *fpp;

COORD coord = {0,0};

int s, b, u;


void gotoxy(int x, int y){
    coord.X = x;
    coord.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);

}
int main(void){
    firstPage();
    return 0;
}
void firstPage(){
    system("cls");
    system("COLOR F0");
    char ch;
    gotoxy(55,23);
    date();
	gotoxy(10,3);
	printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2 Welcome to the DIU Blood Bank \xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(25,8);
    printf("Thanks for using our software.");
    gotoxy(23,13);
    printf("Press 1 if you want to go to Admin Panel.");
    gotoxy(23,15);
    printf("Press 2 for Guest.");

    InputOptions:
        gotoxy(23,18);
        printf("Enter your choice : ");
        ch = getch();
        switch(ch){
        case '1':
            login(1);
            break;
        case '2':
            guest_design();
            break;
        default:
            {
                gotoxy(20,21);
                printf("\aWrong Entry!!Please re-enter the correct output");
                goto InputOptions;
            }
        }
}
void login(int FirstTime){
    system("cls");
    system("COLOR F0");
    gotoxy(55,23);
    date();
    if(FirstTime == 0)
    {
        gotoxy(25,15);
        printf("Password Incorrect.");
    }
    char d[16]=" Login Panel ";
    char ch,pass[10];
    int i=0,j;
    gotoxy(15,4);
    for(j=0;j<15;j++)
    {
        printf("\xB2");
    }
    for(j=0;j<3;j++){
        printf("=");
    }
    for(j=0;j<12;j++)
    {
        printf("%c",d[j]);
    }
    for(j=0;j<3;j++){
        printf("=");
    }
    for(j=0;j<15;j++)
    {
        printf("\xB2");
    }
    gotoxy(25,7);
    printf("Enter Password:");

    while(ch!=13)
    {
        ch=getch();

        if(ch!=13 && ch!=8)
            {
                putch('*');
                pass[i] = ch;
                i++;
            }
    }
    pass[i] = '\0';
    if(strcmp(pass,password)==0)
    {

        gotoxy(25,12);
        printf("Login Successful");
        gotoxy(25,15);
        printf("Press any key to go to main menu");
        if(getch())
        {
        admin_design();
        }
    }
    else
    {
        login(0);
    }
}
void admin_design(){
    system("cls");
    system("COLOR F0");
    int i;
    gotoxy(5,2);
        print_load_slow();
        Sleep(2000);
        for(i=0; i<3; i++)
        {
            system("cls");
            gotoxy(5,2);
            printf("Admin Panel......\n\n\n");
            Sleep(500);
            gotoxy(5,4);
            print_admin();
            Sleep(500);

        }
        admin_mainmenu();
}
void admin_mainmenu(){
    char c;
    system("cls");
    system("COLOR F0");
    gotoxy(55,23);
    date();
    gotoxy(15,3);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2 MAIN MENU \xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(15,4);
    printf("\xB2\t\t\t\t\t\t\xB2");
    gotoxy(15,5);
    printf("\xB2\t\t1. Add New Donor\t\t\xB2");
    gotoxy(15,6);
    printf("\xB2\t\t2. View Blood Donor\t\t\xB2");
    gotoxy(15,7);
    printf("\xB2\t\t3. Delete Donor\t\t\t\xB2");
    gotoxy(15,8);
    printf("\xB2\t\t4. Logout\t\t\t\xB2");
    gotoxy(15,9);
    printf("\xB2\t\t5. Exit\t\t\t\t\xB2");
    gotoxy(15,10);
    printf("\xB2\t\t\t\t\t\t\xB2");
    gotoxy(15,11);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");


    InputOptions:
        gotoxy(20,15);
        printf("Enter your choice: ");
        c = getch();
        switch(c)
        {
        case '1':
            newdonor();
            break;
        case '2':
            viewdonor();
            break;
        case '3':
            deletedonor();
            break;
        case '4':
            firstPage();
            break;
        case '5':
            system("cls");
            exit(0);
        default:
            {
                system("cls");
                gotoxy(20,18);
                printf("\aWrong Entry!!Please re-enter the correct output");
                goto InputOptions;
            }
        }
}
void newdonor(){
    char c;
    system("cls");
    system("COLOR F0");
    gotoxy(55,23);
    date();
    gotoxy(15,3);
    printf("******************** Add New Blood Donor ********************");
    gotoxy(23,5);
    printf("1. A+");
    gotoxy(23,6);
    printf("2. A-");
    gotoxy(23,7);
    printf("3. B+");
    gotoxy(23,8);
    printf("4. B-");
    gotoxy(23,9);
    printf("5. AB+");
    gotoxy(23,10);
    printf("6. AB-");
    gotoxy(23,11);
    printf("7. O+");
    gotoxy(23,12);
    printf("8. O-");
    gotoxy(15,14);
    printf("**************************************************************");
    gotoxy(23,16);
    printf("Choose your category to add Donor: ");
    scanf("%d", &s);

    fp=fopen("donor.dat","ab+");
    if(getdata()==1)
    {
        donor.cat=catagories[s-1];
        fseek(fp,0,SEEK_END);
        fwrite(&donor,sizeof(donor),1,fp);
        fclose(fp);
        gotoxy(21,17);
        printf("Account Created successfully!");
        gotoxy(21,19);
        printf("Enter 1 to go to the Main menu OR 0 for Exit");
        scanf("%d", &b);
        if (b==1)
            admin_mainmenu();
        else
            system("cls");
            exit(0);
    }
}
int getdata(){
    system("cls");
    system("COLOR F0");
    int b, t;
    gotoxy(20,5);printf("Enter the Information Below");
	gotoxy(15,6);
	printf("********************************************");
	gotoxy(15,15);
	printf("********************************************");
    gotoxy(28,8);
    printf("Category:");
	gotoxy(38,8);
	printf("%s",catagories[s-1]);
	InputData:
    gotoxy(21,10);
    printf("Enter Donor ID number: ");
    scanf("%d",&t);
    if (checkid(t)==0){
        gotoxy(21,19);
        printf("This ID already exists. Input again!");
        goto InputData;
        return 0;
    }
    donor.donor_id=t;
    gotoxy(21,11);
    printf("Enter Donor Name: ");
    scanf("%s", donor.name);
    gotoxy(21,12);
    printf("Enter Donor Address: ");
    scanf("%s", donor.address);
    gotoxy(21,13);
    printf("Enter Donor Phone Number: ");
    scanf("%d", &donor.phone);
    gotoxy(21,14);
    printf("Enter Donor Email: ");
    scanf("%s", donor.email);
    return 1;
}
int  checkid(int t){
    rewind(fp);
    while(fread(&donor,sizeof(donor),1,fp)==1)
        if(donor.donor_id == t)
        return 0;           //returns 0 if user exits
    return 1;
}
void viewdonor(){
    int i=0,j;
    system("cls");
    system("COLOR F0");
    gotoxy(1,1);
    printf("*********************************Donor List*****************************");
    gotoxy(2,2);
    printf("  ID    TYPE    NAME        CONTACT        Address        EMAIL    ");
    j=4;
    fp=fopen("donor.dat","rb");
    while(fread(&donor,sizeof(donor),1,fp)==1)
    {
        gotoxy(4,j);
        printf("%d",donor.donor_id);
        gotoxy(10,j);
        printf("%s", donor.cat);
        gotoxy(18,j);
        printf("%s",donor.name);
        gotoxy(30,j);
        printf("%d", donor.phone);
        gotoxy(45,j);
        printf("%s",donor.address);
        gotoxy(60,j);
        printf("%s",donor.email);
        printf("\n\n");
        j++;
    }
    fclose(fp);
    gotoxy(35,25);
    printf("Press any key to return to main menu");
    if(getch())
        admin_mainmenu();
}
void deletedonor(){
    int findonor;
   	system("cls");
    system("COLOR F0");
   	int d, j = 12;
   	char name[30];
   	char another='y';
   	while(another=='y')
   	{
		system("cls");
		gotoxy(24,1);
		printf("Enter the Information Below");
        gotoxy(15,3);
        printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
        gotoxy(15,7);
        printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
		gotoxy(23,5);
		printf("Enter the Donor ID for delete:");
		scanf("%d",&d);
		fp=fopen("donor.dat","rb");
		rewind(fp);
		while(fread(&donor,sizeof(donor),1,fp)==1)
		{
			if(donor.donor_id==d)
	 		{
	 		    gotoxy(23,9);
	 		    printf("Donor record is available");
	 		    gotoxy(10,11);
                printf("TYPE    NAME        Address        EMAIL    PHONE NUMBER");
	 		    gotoxy(11,j);
                printf("%s",donor.cat);
                gotoxy(18,j);
                printf("%s",donor.name);
                gotoxy(30,j);
                printf("%s", donor.address);
                gotoxy(45,j);
                printf("%s", donor.email);
                gotoxy(55,j);
                printf("%d",donor.phone);
                findonor=0;
				break;
			}
		}
		if(findonor==0 )
		{
		    gotoxy(15,16);
		    printf("Do you want to delete it?(Y/N):");
		    if(getch()=='y')
			{
				fpp=fopen("blood.dat","wb");
				rewind(fp);
				while(fread(&donor,sizeof(donor),1,fp)==1)
				{
					if(donor.donor_id!=d)
		 			{
						fseek(fpp,0,SEEK_CUR);
						fwrite(&donor,sizeof(donor),1,fpp);
					}
				}
                fclose(fpp);
                fclose(fp);
                int a=1;

                a=remove("donor.dat");

                rename("blood.dat","donor.dat");
                if(a==0)
                {
                    gotoxy(15,18);
                    printf("This account is successfully deleted");
                    gotoxy(15,20);
                    printf("Delete another Account?(Y/N)");
                }
			}
            else
                admin_mainmenu();
				fflush(stdin);
				another=getch();
        }
        else
        {
            gotoxy(15,16);
            printf("No record is found.");
            if(getch())
            admin_mainmenu();
        }
    }
	admin_mainmenu();
}
void guest_design(){
    system("cls");
    system("COLOR F0");
    int i;
    gotoxy(5,2);
        print_load_slow();
        Sleep(2000);
        for(i=0; i<3; i++)
        {
            system("cls");
            gotoxy(5,2);
            printf("Welcome Guest......\n\n\n");
            Sleep(500);
            gotoxy(5,4);
            print_admin();
            Sleep(500);

        }
        guest_mainmenu();
}
void guest_mainmenu(){
    char c;
    system("cls");
    system("COLOR F0");
    gotoxy(55,23);
    date();
    gotoxy(15,3);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2 Guest Menu \xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(15,10);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(15,4);
    printf("\xB2\t\t\t\t\t\xB2");
    gotoxy(15,9);
    printf("\xB2\t\t\t\t\t\xB2");
    gotoxy(15,5);
    printf("\xB2\t\t1. View Donor\t\t\xB2");
    gotoxy(15,6);
    printf("\xB2\t\t2. Contact us\t\t\xB2");
    gotoxy(15,7);
    printf("\xB2\t\t3. Back\t\t\t\xB2");
    gotoxy(15,8);
    printf("\xB2\t\t4. Exit\t\t\t\xB2");
    gotoxy(23,12);
    printf("Select Choice : ");
    scanf("%d", &u);
    if(u == 1){
        searchdonor();
    }else if(u == 2){
        contact();
    }else if (u == 3){
        firstPage();
    }else if (u == 4){
        system("cls");
        exit(0);
    }else{
        guest_mainmenu();
    }
}
void contact(){
    system("cls");
    system("COLOR F0");
    gotoxy(55,23);
    date();
    gotoxy(15,3);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2 Admin Contact \xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(15,8);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(15,4);
    printf("\xB2  \t\t\t\t\t   \xB2");
    gotoxy(15,7);
    printf("\xB2\t\t\t\t\t   \xB2");
    gotoxy(15,5);
    printf("\xB2\tName : Rubaiyat Tasnia Husain\t   \xB2");
    gotoxy(15,6);
    printf("\xB2\tEmail : rubaiyat229@gmail.com\t   \xB2");
    gotoxy(35,25);
    printf("Press any key to return to main menu");
    if(getch())
        guest_mainmenu();
}
void searchdonor(){

    int i=0,j, z=1;
    system("cls");
    system("COLOR F0");
    gotoxy(1,1);
    printf("\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2 Donor List \xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2\xB2");
    gotoxy(2,2);
    printf(" Donor    TYPE    NAME        CONTACT        Address        EMAIL    ");
    j=4;
    fp=fopen("donor.dat","rb");
    while(fread(&donor,sizeof(donor),1,fp)==1)
    {
        gotoxy(4,j);
        printf("%d",z);
        gotoxy(13,j);
        printf("%s", donor.cat);
        gotoxy(21,j);
        printf("%s",donor.name);
        gotoxy(33,j);
        printf("%d", donor.phone);
        gotoxy(48,j);
        printf("%s",donor.address);
        gotoxy(63,j);
        printf("%s",donor.email);
        printf("\n\n");
        j++;
        z++;
    }
    fclose(fp);
    gotoxy(35,25);
    printf("Press any key to return to main menu");
    if(getch())
        guest_mainmenu();
}
void print_load_slow(){

    system("COLOR F0");
    printf("Loading......\n\n\n");
}
void print_admin(){

    system("COLOR F0");
    printf("...");
}
void date(){
    time_t current_time;
    char* c_time_string;
    current_time=time(NULL);
    c_time_string=ctime(&current_time);
    print_slow(c_time_string);
}
void print_slow(char per[1000]){
    int m,n;
    n=strlen(per);
    for(m=0; m<n; m++)
    {
        if(per[m]==' ')
        {
            printf("%c", per[m]);
            continue;
        }
        else
        {
            Sleep(speed);
            printf("%c", per[m]);
        }
    }
}
