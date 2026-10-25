 #include<stdio.h>
 #include<conio.h>
 #include<process.h>
//----------------------------------------------
 struct Bank
  {
    int acno;
    char name[20];
    char address[20];
    float balance;
  }b;
//----------------------------------------------
 FILE *fp;
//----------------------------------------------
 void NewAccount();
 void ShowRecords();
 void SearchRecord();
 void DeleteRecord();
 void ModifyRecord();
 void Deposite();
 void Withdrawal();
 void Login();
 int GenerateAccountNo();
 int CheckAccount(int);
//----------------------------------------------
 void main()
  {
   int ch;
   clrscr();
   Login();
   while(1)
    {
	clrscr();
	printf("\n Welcome To SBI Bank, Satara");
	printf("\n------------------------------------------");
	printf("\n 1. New Account");
	printf("\n 2. Show Account");
	printf("\n 3. Search Account");
	printf("\n 4. Modify Account");
	printf("\n 5. Delete Account");
	printf("\n 6. Deposite");
	printf("\n 7. Withdrawal");
	printf("\n 8. Exit");
	printf("\n------------------------------------------");
	printf("\n Enter Your Choice = ");
	scanf("%d",&ch);
	printf("------------------------------------------");
	if(ch==1)
	  NewAccount();
	else if(ch==2)
	  ShowRecords();
	else if(ch==3)
	  SearchRecord();
	else if(ch==4)
	  ModifyRecord();
	else if(ch==5)
	  DeleteRecord();
	else if(ch==6)
	  Deposite();
	else if(ch==7)
	  Withdrawal();
	else if(ch==8)
	  exit(0);
	getch();
     }
  }
//----------------------------------------------
  int GenerateAccountNo()
   {
     int n = 0;
     fp = fopen("bank.txt","r");
     while( fread(&b,sizeof(b),1,fp)!=NULL)
      {
       n = b.acno;
      }
     fclose(fp);
     return (n+1);
   }
//----------------------------------------------
 int CheckAccount(int x)
  {
   int flg = 0;
   fp = fopen("bank.txt","r");
   while( fread(&b,sizeof(b),1,fp)!=NULL)
    {
     if(b.acno==x)
      {
       flg = 1;
       break;
      }
    }
   fclose(fp);
   return flg;
  }
//----------------------------------------------
 void NewAccount()
  {
   b.acno = GenerateAccountNo();
   printf("\n Account No = %d",b.acno);
   printf("\n Enter Name       = ");
   scanf("%s",&b.name);
   printf(" Enter Address    = ");
   scanf("%s",&b.address);
   printf(" Enter Balance    = ");
   scanf("%f",&b.balance);
   fp = fopen("bank.txt","ab");
   fwrite(&b,sizeof(b),1,fp);
   fclose(fp);
   printf("------------------------------------------");
   printf("\n Account Created Successfully...");
  }
//----------------------------------------------------------------
 void ShowRecords()
  {
   fp = fopen("bank.txt","rb");

   printf("\n Account No  Name    Address  Balance");
   printf("\n------------------------------------------");
   while(fread(&b,sizeof(b),1,fp)!=NULL)
    {
     printf("\n %d   %s   %s   %f",b.acno,b.name,b.address,b.balance);
    }
   printf("\n------------------------------------------");
   fclose(fp);
  }
//----------------------------------------------------------------
 void SearchRecord()
  {
   int n,flg;
   printf("\n Enter Account No To Search Record = ");
   scanf("%d",&n);
   flg = CheckAccount(n);
   if(flg==0)
    {
     printf("\n Such Account Does Not Exist...");
     return;
    }
   fp = fopen("bank.txt","rb");
   while( fread( &b, sizeof(b), 1, fp)!=NULL)
    {
      if(b.acno==n)
       {
	printf("\n Account No = %d",b.acno);
	printf("\n Name       = %s",b.name);
	printf("\n Address    = %s",b.address);
	printf("\n Balance    = %f",b.balance);
	break;
       }
    }
   fclose(fp);
  }
//----------------------------------------------------------------
 void DeleteRecord()
  {
   FILE *fp1;
   int n,flg;
   printf("\n Enter Account No To Delete Record = ");
   scanf("%d",&n);
   flg = CheckAccount(n);
   if(flg==0)
    {
     printf("\n Such Account Does Not Exist...");
     return;
    }
   fp = fopen("bank.txt","rb");
   fp1 = fopen("demo.txt","wb");

   while( fread( &b, sizeof(b), 1, fp)!=NULL)
    {
      if(b.acno!=n)
	fwrite( &b, sizeof(b), 1, fp1);
    }
   fclose(fp);
   fclose(fp1);
   remove("bank.txt");
   rename("demo.txt","bank.txt");
   printf("\n Record Deleted Successfully...");
  }
//----------------------------------------------------------
  void ModifyRecord()
   {
   }
//----------------------------------------------------------
  void Deposite()
   {
   }
//----------------------------------------------------------
  void Withdrawal()
   {
   }
//----------------------------------------------------------
  void Login()
   {
   }
