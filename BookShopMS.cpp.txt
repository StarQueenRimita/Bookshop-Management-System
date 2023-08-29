#include<iostream>
#include<fstream>
#include<stdlib.h>
#include<string>
using namespace std;

int strtoint(string s){
	int i = 0;
    for (int a =0; a<s.size(); a++) {
    	char c = s[a];
        i = i * 10 + (c - '0');
    }
    //cout<<i<<endl;
    return i;
}

class bookshop{
    public:
    void ControlPanel();
    void AddBook();
    void UpdateBook();
    void DeleteBook();
    void ShowBook();
    void CheckBook();
};

void bookshop::ControlPanel(){
    while(1){
    	system("cls");                     //clear screen
	    cout<<"--------------------CONTROL PANEL--------------------\n"<<endl;
	    cout<<"\t1.\tAdd Book"<<endl;
	    cout<<"\t2.\tUpdate Book"<<endl;
	    cout<<"\t3.\tDelete Book"<<endl;
	    cout<<"\t4.\tDisplay Books"<<endl;
	    cout<<"\t5.\tCheck Book"<<endl;
	    cout<<"\t6.\tEXIT"<<endl;
	    cout<<"\n\t\t\tEnter your choice:\t";
	    
    	int a;
    	cin>>a;
    	switch(a){
    		case 1:{
    			AddBook();
				break;
			}
			case 2:{
				UpdateBook();
				break;
			}
			case 3:{
				DeleteBook();
				break;
			}
			case 4:{
				ShowBook();
				break;
			}
			case 5:{
				CheckBook();
				break;
			}
			case 6:{
				exit(0);
				break;
			}
			default:{
				cout<<"\n\t\t\t\t\tPlease enter a valid option!"<<endl;
			}
		}
	}
}

void bookshop::AddBook(){
    system("cls");   
    string n, bid;
    string bname, anamef, anamel;
    cin.ignore();
    cout<<"Enter the book to be added (in one word):"<<endl;
    cout<<"Book name:\t";
    cin>>bname;
    cin.ignore();
    cout<<"Book ID:\t";
    cin>>bid;
    cin.ignore();
    cout<<"Author First name:\t";
    cin>>anamef;
    cin.ignore();
    cout<<"Author Last name:\t";
    cin>>anamel;
    cin.ignore();
    cout<<"No. of copies:\t";
    cin>>n;
    fstream file;
    file.open("book.csv",ios::out | ios::app);
    file<<bid<<","<<bname<<","<<anamef<<","<<anamel<<","<<n<<endl;
    file.close();
    system("pause");
}

void bookshop::UpdateBook(){
    system("cls");
    fstream file, file1;
    string bname, anamef, anamel, bbname, aanamef, aanamel;
    string n, nn, bid, bbid;
	int count=0;
    file.open("book.csv",ios::in );
    file1.open("book1.csv", ios::out | ios::app);
    if(!file){
        cout<<"File doesn't exist!!!!"<<endl<<endl;
    }
    else{
        cout<<"Enter the Book ID:\t";
        cin>>bid;
        //file>>bbid>>bbname>>aanamef>>aanamel>>nn;
        while(getline(file, bbid, ',')){
        	getline(file, bbname, ',');
        	getline(file, aanamef, ',');
        	getline(file, aanamel, ',');
        	getline(file, nn, '\n');
        	
            if(bbid==bid){
            	cin.ignore();
                cout<<"Enter the updated data:"<<endl;
                cout<<"Book name:\t";
			    cin>>bname;
			    cin.ignore();
                cout<<"Author First name:\t";
			    cin>>anamef;
			    cin.ignore();
			    cout<<"Author Last name:\t";
			    cin>>anamel;
			    cin.ignore();
			    cout<<"No. of copies:\t";
			    cin>>n;
                file1<<bid<<","<<bname<<","<<anamef<<","<<anamel<<","<<n<<endl;
                count++;
            }
            else{
                file1<<bbid<<","<<bbname<<","<<aanamef<<","<<aanamel<<","<<nn<<endl;
                //file>>bbid>>bbname>>aanamef>>aanamel>>nn;
            }
        }
        if(count==0){
            cout<<"Book ID "<< bid <<" not found!!"<<endl;
        }
        system("pause");
        file.close();
        file1.close();
        remove("book.csv");
        rename("book1.csv", "book.csv");
    }
}

void bookshop::DeleteBook(){
    system("cls");
    fstream file, file1;
    string bname, aname, bbname, aanamef, aanamel, n, nn, bid, bbid;
	int count=0;
    file.open("book.csv", ios::in);
    file1.open("book1.csv", ios::out | ios::app);
    if(!file){
        cout<<"File doesn't exist!!!!"<<endl<<endl;
    }
    else{
        cout<<"Enter the Book ID:\t";
        cin>>bid;
        //file>>bbid>>bbname>>aanamef>>aanamel>>nn;
        while(getline(file, bbid, ',')){
        	getline(file, bbname, ',');
        	getline(file, aanamef, ',');
        	getline(file, aanamel, ',');
        	getline(file, nn, '\n');
            if(bbid!=bid){
                file1<<bbid<<", "<<bbname<<", "<<aanamef<<", "<<aanamel<<", "<<nn<<endl;
                //file>>bbid>>bbname>>aanamef>>aanamel>>nn;
            }
            else if(bbid==bid){
            	count=1;
			}
        }
        if(count==0){
            cout<<"Book ID "<< bid <<" not found!!"<<endl;
        }
        system("pause");
        file.close();
        file1.close();
        remove("book.csv");
        rename("book1.csv", "book.csv");
    }
}

void bookshop::ShowBook(){
    system("cls");
    fstream file;
    file.open("book.csv");
    string bname,anamef, anamel;
    string n,bid;
    if(!file){
        cout<<"File doesn't exist!!!!"<<endl<<endl;
    }
    else{
    	cout << "\n------------------------------------SHOWING BOOKS------------------------------------" << endl;
		cout << "\n-------------------------------------------------------------------------------------" << endl;

        cout<<"\tBook ID\t\tBook name\t\tAuthor's Name\t\tNo. of Copies"<<endl;
        while(getline(file, bid, ',')){ // use getline as the condition
        	getline(file, bname, ',');
        	getline(file, anamef, ',');
        	getline(file, anamel, ',');
        	getline(file, n, '\n');
            cout<<"\t"<<bid<<"\t\t"<<bname<<"\t\t"<<anamef<<" "<<anamel<<"\t\t"<<n<<endl;
        }
        cout << "\n-------------------------------------------------------------------------------------" << endl;

    }
    file.close();
    system("pause");
}

void bookshop::CheckBook(){
    system("cls");
    fstream file;
    string bname, anamef, anamel, bbname, aanamef, aanamel;
    string n, nn, bid, bbid;
	int count=0;
    file.open("book.csv");
    if(!file){
        cout<<"File doesn't exist!!!!"<<endl<<endl;
    }
    else{
        int flag=0;
        cout<<"Enter the Book ID:\t";
        cin>>bid;
        while(getline(file, bbid, ',')){
        	getline(file, bbname, ',');
        	getline(file, aanamef, ',');
        	getline(file, aanamel, ',');
        	getline(file, nn, '\n');
            if(bid==bbid){
                flag=1;
                //cout<<nn;
                if(stoi(nn)==0){
                    cout<<"Book is Out of Stock!!!!"<<endl;
                }
                else{
                    cout<<"Book ID:\tBook name\tAuthor's name\t\tNo. of copies\n";
                    cout<<bbid<<"\t\t"<<bbname<<"\t"<<aanamef<<" "<<aanamel<<"\t"<<nn<<endl;
                }
            }
        }
        if(flag==0){
            cout<<"Book doesn't exist!!!!"<<endl;
        }
    }
    file.close();
    system("pause");
}

int main(){
    bookshop ob;
    ob.ControlPanel();
    return 0;
}