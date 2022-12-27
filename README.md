# ATM_Management_System
ATM management system using C++ object oriented concepts. 

#include <conio.h>
#include <iostream>
#include <string>
using namespace std;
class ATM
{
	protected:
		long int account_no;
        string name;
        int PIN;
        int amount=100000;
        int n;
        public:
        //Virtual function is added here. This type of polymorphism is achieved by Function Overriding.                                   
        virtual void display(){
            cout<<"Account no is "<<account_no<<endl;
            cout<<"Name is "<<name<<endl;
            cout<<"PIN is "<<PIN<<endl;
            cout<<"Amount withdrawn is "<<n<<endl;
}
  
};


class balanceinquiry : public ATM     // Inheritance
{
	private:
		long int account_no;                  
        string name;
        int PIN;                 //The variables account_no, name, and  PIN are private.
		                         // This means that they can be accessed only by other members 
							     //of the class, and not by any other part of your program.
								 // This is one way encapsulation is achieved.
    public:
    	void getdata()
    	{
    		cout<<"Please enter account number: ";
    		cin>>account_no;
    		cout<<"Please enter account holder: ";
    		cin>>name;
    		cout<<"Please enter PIN: ";
    		cin>>PIN;                            
		}                        
		void balance(int amount)
		{
			
			cout<<"The total bank balance is: "<<amount<<endl;
		}
    
        void display()
        {
        	cout<<endl<<"**BALANCE INQUIRY**"<<endl;
        	cout<<"Amount left is: "<<amount<<endl;
		}                    //Above class gives information about balance.
		                    // The public members getdata, balance and display are the interfaces
							// to the outside world and a user needs to know them to use the class.
							// The private member account_no, name and PIN is something that is hidden from the outside world,
							// but is needed for the class to operate properly.
		
};
class userdetails: public ATM     // Inheritance
{
	private:
		long int account_no;
        string name;
        int PIN;
        int amount=100000;
    public:
    	void getdata()
    	{
    		cout<<"Please enter account number: ";
    		cin>>account_no;
    		cout<<"Please enter account holder: ";
    		cin>>name;
    		cout<<"Please enter PIN: ";
    		cin>>PIN;
		}
		
		void display()
		{
			cout<<endl<<"**USER DETAILS**"<<endl;
			cout<<"Your account number is: "<<account_no<<endl;
			cout<<"Account holder is: "<<name<<endl;
			cout<<"Your PIN is: "<<PIN<<endl;
			cout<<"You have "<<amount<<" in you account."<<endl;
		}
};
class cashwithdrawal: public ATM      // Inheritance
{
	
	private:
		long int account_no;
        string name;
        int PIN;
        int n;
        int amount=100000;
    public:
    	void getdata()
    	{
    		cout<<"Please enter account number: ";
    		cin>>account_no;
    		cout<<"Please enter account holder: ";
    		cin>>name;
    		cout<<"Please enter PIN: ";
    		cin>>PIN;
    		cout<<"Enter amount to be withdrawn: ";
    		cin>>n;
		}
		void display()
		{
			cout<<endl<<"**CASH WITHDRAWAL**"<<endl;
			cout<<"Amount to withdraw is: "<<n<<endl;
			cout<<"Total amount left behind is: "<<amount-n<<endl;
			cout<<"Thankyou for the transaction!!!"<<endl;
		}        
};

//Two classes (Deposit and user) has been made to demonstrate composition.

class Deposit{
	public:
		int deposit_amount;
		Deposit(){}
		void deposit1(int da){
			deposit_amount = da;
		}
};

class user{
	public:
	long int account_no;
	int PIN;
	int amount=100000;
	Deposit D;        //Composition. Object of different class has been made in class instead of in int main().
	user(){}
	user(long int acc, int pin, int a, int da){
		account_no=acc;
		PIN=pin;
		D.deposit1(da);
	}
	void getdeposit(){
		cout<<"Enter your account number: "<<endl;
		cin>>account_no;
		cout<<"Enter your PIN: "<<endl;
		cin>>PIN;
		cout<<"Enter amount to deposit: "<<endl;
		cin>>D.deposit_amount;
	}

	void showbalance(){
		cout<<endl<<"Your balance before depositing: "<<amount<<endl;
		cout<<"Your balance after depositing: "<<amount + D.deposit_amount<<endl;
	}

};


int main()
{
	int choice;
	cout<<endl<<"**WELCOME TO ATM MANAGEMENT SYSTEM**"<<endl;

	while(1){
    cout<<endl<<"Select from options."<<endl;
	cout<<"1. Balance Inquiry."<<endl;
	cout<<"2. User Details."<<endl;
	cout<<"3. Cash Withdrawal."<<endl;
	cout<<"4. Deposit."<<endl;
	cout<<"5. Exit."<<endl;

	cout<<"Enter number (1), (2), (3), (4) or (5)"<<endl;
	cout<<endl;
	cin>>choice;
	if (choice==1)
	{
        //Virtual function, binded at runtime (Runtime polymorphism)
        balanceinquiry * balance_ptr;                
		balanceinquiry b1;
        balance_ptr = & b1;
        balance_ptr -> getdata();
        balance_ptr -> display();
	}
	else if(choice==2)
	{
        userdetails * userdetails_ptr;
		userdetails d1;
        userdetails_ptr = &d1;
        userdetails_ptr ->getdata();
        userdetails_ptr ->display();
	}
	else if(choice==3)
	{
		cashwithdrawal c1;
        c1.getdata();
        c1.display();
     
    }
	else if(choice==4){
		user u;
		u.getdeposit();
		u.showbalance();
	}
    else if (choice==5){
        exit(0);
    }
	
}

	return 0;
	
}