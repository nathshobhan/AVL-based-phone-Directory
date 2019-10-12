#include<string.h>
#include<iostream>
#include<cstdlib>
#include<stdio.h>
#include<fstream>
#include<iomanip>
#include<windows.h>
using namespace std;
void printer(char x[],char y[]){
    cout<<(char)186<<setw(20)<<x<<(char)186<<setw(20)<<y<<(char)186<<endl;
}
void endd(){
    int i;
    cout<<(char)200;
    for( i=0;i<20;i++)
        cout<<(char)205;
    cout<<(char)202;
    for(int i=0;i<20;i++)
        cout<<(char)205;
    cout<<(char)188;
}


class node
{
public:
	char name[128] , contact[256];
	class node *left;
	class node *right;
	int ht;
};

class tree
{
public:
	node* root;
	node* insert_node(char* , char* , node*);
	void inorder(node*);
	void insertfile(node*);
	int search(node* , char*);
	node * min(node *);
	node* delete_node(node* , char*);
	int update(node* , char*);
	int height(node *);
	int BF(node*);
	node * LR(node*);
	node * LL(node*);
	node * RL(node*);
	node * RR(node*);
	node * rotateleft(node*);
	node* rotateright(node*);
	tree()
	{
		root=NULL;
	}
};

int tree :: height(node* T)//height of the node
{
	int lh , rh;
	if(T->left==NULL)
		lh=0;
	else
		lh=1+T->left->ht;
	if(T->right==NULL)
		rh=0;
	else
		rh=1+T->right->ht;
	if(lh>rh)
		return lh;
	return rh;
}

int tree :: BF(node*T)
{
	int lh , rh;
	if(T==NULL)
		return 0;
	if(T->left==NULL)
		lh=0;
	else
		lh=1+T->left->ht;
	if(T->right==NULL)
		rh=0;
	else
		rh=1+T->right->ht;
	return (lh-rh);
}

node * tree :: RR(node *T)
{
	T=rotateleft(T);//rotate the node T towards left
	return T;
}
node * tree :: LL(node *T)
{
	T=rotateright(T);
	return T;
}

node * tree :: LR(node* T)//Right of left or Left ka right
{
		T->left=rotateleft(T->left);//left rotation
		T=rotateright(T);
		return T;
}

node * tree :: RL(node* T)//left of right or Right ka left
{
		T->right=rotateright(T->right);//left rotation
		T=rotateleft(T);
		return T;
}

node * tree :: rotateright(node* x)
{
	node *y ;
	y=x->left;
	x->left=y->right;
	y->right=x;
	x->ht=height(x);//height of node x
	y->ht=height(y);//height of node y
	return y;//rotated node(newly formed node)
}

node * tree :: rotateleft(node* x)
{
	node *y ;
	y=x->right;
	x->right=y->left;
	y->left=x;
	x->ht=height(x);//height of node x
	y->ht=height(y);//height of node y
	return y;//rotated node(newly formed node)
}

node * tree :: min(node *q)
{
	while(q->left != NULL)
	{
		q = q->left;
	}
	return q;
}
node* tree :: insert_node(char* name , char* contact , node* T)
{

	int cmp;
	if(T==NULL)
	{
		//creating root
		T=new node;
		T->left=NULL;
		T->right=NULL;
		strcpy(T->name , name);
		strcpy(T->contact , contact);

	}
	else
	{
		cmp=strcasecmp( name , T->name);
		if(cmp<0)//means if the entered element is less than the current element so cmp will contains value less than 0
			{
				T->left=insert_node(name , contact ,T->left);
				if(BF(T)==2)
				{
					if(strcasecmp( name , T->left->name)<0)
						T=LL(T);
					else
						T=LR(T);
				}
			}

		else if(cmp>0)
		{
			T->right =insert_node(name ,contact , T->right);
			if(BF(T)==-2)
			{
				if(strcasecmp( name , T->right->name)>0)
					T=RR(T);
				else
					T=RL(T);
			}

		}
		else
		{
			cout<<"ELEMENT REPEATED!!!"<<endl;
		}
	}
		T->ht=height(T);

return T;
}

void tree ::inorder(node* head)//LVR
{
	fstream i;
	if(head!=NULL) //if recursion then we will use if
	{
		inorder(head->left);
		i.open("file.txt", ios::in | ios::out | ios::app);
		i<<head->name<<" "<<head->contact<<"\n";
		i.close();
		printer(head->name,head->contact);
		inorder(head->right);
	}

}
int tree :: search(node* head , char *str)
{

	while(head!=NULL)
	{
		int cmp=strcasecmp( str , head->name);
		if(cmp==0)
		{
			cout<<"\n\ncontact is :\t"<<head->contact<<endl;
			return 1;

		}
		else if(cmp<0)
			{
				head=head->left;
			}
		else if(cmp>0)
		{
			head=head->right;
		}

	}

	return -1;
}

node* tree :: delete_node(node* T , char* str )
{
	node *temp;
	int cmp;
	cmp=strcasecmp(str , T->name);//the value which is to be compared will be in the left side and with which the value is compared will be in right hand side
	if(T==NULL)
	{
			cout<<"Phone Directory not created"<<endl;
			return T;
	}

	else if(cmp<0)
		{
			T->left=delete_node(T->left , str);
			if(BF(T)==-2)
			{
				if(BF(T->right)<=0)
				T=RR(T);
				else
				T=RL(T);
			}
		}

		else if(cmp>0)
				{
					T->right=delete_node(T->right , str);
					if(BF(T)==2)
					{
						if(BF(T->left)>=0)
						T=LL(T);
						else
						T=LR(T);
					}
				}
		else
		{
			if(T->right!=NULL)
			{
				temp=T->right;
				while(temp->left!=NULL)
					temp=temp->left;
				strcpy(T->name , temp->name);
				strcpy(T->contact , temp->contact);
				T->right=delete_node(T->right , temp->name);
				if(BF(T)==2)
				{
					if(BF(T->left)>=0)
						T=LL(T);
					else
						T=LR(T);

				}
			}
			else
			{
				return T->left;
				cout<<"\nsorry entered element not found\n"<<endl;

			}

		}
	T->ht=height(T);
	return T;
}

int tree :: update(node* head , char* name)
{
	char meanng[256];
	while(head!=NULL)
	{
		int cmp;
		cmp=strcasecmp( name , head->name );
		if(cmp==0)
		{
			cout<<"Enter the  new contact"<<endl;
			cin>>meanng;
			strcpy(head->contact , meanng);
			cout<<"Value updated"<<endl;
			return 1;
		}
		if(cmp<0)
			head=head->left;
		if(cmp>0)
			head=head->right;

	}

return 0;
}

int main()
{
	char str[128] , contact[256];
	node * head;
	head=NULL;
	int ch , rtrn;
	char c;
	tree t1;
	fstream  fp;
	fp.open("file.txt", ios::in);


	char data[256];
	if(!fp)
	{
		cout<<"Error in opening file"<<endl;
	}
	  else
	  {
		  while(fp>>data)
	      {

	          strcpy(str,data);
	          fp>>contact;
	            if(strcmp(data,"")!=0)
	            {
	                 head = t1.insert_node( str , contact, head);
	            }
	      }
	  }
	 fp.close();


	do
	{
		cout<<"\n  PERSONAL PHONE DIRECTORY"<<endl;
		cout<<"-------------------------------"<<endl;
		cout<<"\n1. INSERT NEW NUMBER\n2. DISPLAY ALL NUMBERS\n3. SEARCH CONTACT NUMEBR BY NAME\n4. DELETE CONTACT NUMBER\n5. UPDATE NUMBER BY NAME\n6. EXIT"<<endl;
		cout<<"\n\nENTER OPERATION NUMBER : "<<endl;
		cin>>ch;
		switch(ch)
		{
			case 1:	cout<<"\nEnter Name to be Inserted in Directory : ";
					cin>>str;
					cout<<"Enter Contact Number of '"<<str<<"' : ";
					cin>>contact;
					head = t1.insert_node( str , contact, head);
					break;

			case 2: if(head!=NULL)
				 	{
						system("cls");
						cout<<"\nContacts Present in the Directory are:"<<endl;
						remove("file.txt");
						t1.inorder(head);
				 		endd();
					 }
				 	else
				 	cout<<"\nOOPS!!! DIRECTORY IS EMPTY .... INSERT NUMBERS FIRST"<<endl;
				 	break;

			case 3: cout<<"Enter Name to Find Contact"<<endl;
					cin>>str;
					rtrn =t1.search(head , str);
					if(rtrn==1)
					cout<<"\nCONTACT FOUND !!!"<<endl;
					else
					{
						cout<<"OOPS!! CONTACT DOESNOT EXISTS"<<endl;
					}
					break;

			case 4: cout<<"Enter Contact to be Deleted"<<endl;
				 	cin>>str;
				 	rtrn =t1.search(head , str);
				 	if(head==NULL)
				 	{
					 	cout<<"\nOOPS!!! DIRECTORY IS EMPTY .... INSERT NUMBERS FIRST"<<endl;
				 	}
				 	else if(head!=NULL && rtrn ==1)
					 	head= t1.delete_node(head , str);
				 	else
						cout<<"\nOOPS!! CONTACT DOESNOT EXISTS"<<endl;
				 	break;

			case 5: cout<<"Enter Name to Update its Contact Number"<<endl;
				    cin>>str;
				 	rtrn =t1.update(head , str);
				 	if(rtrn==1)
					 	cout<<"\n"<<str<<" updated"<<endl;
				 	else
					 	cout<<"\nOOPS!! CONTACT DOES NOT EXISTS"<<endl;
				 	break;

			case 6: if(head!=NULL)
					{
						remove("file.txt");
						system("cls");
				 		t1.inorder(head);
				 		endd();
				 		cout<<"\nENTER ANY KEY....";
					}

				 	break;

			default: cout<<"\nOOPS!! YOU HAVE ENTERED INVALID CHOICE"<<endl;

		}
		system("cls");
	}while(ch!=6);
	return 0;
}
