# CODE
This is the code for binary search tree basic operations.
#include<iostream>
using namespace std;
struct node* insert(struct node*,int );
int height(struct node*);
void levelorder(struct node *);
void preorder(struct node* );
void postorder(struct node*);
void inorder(struct node*);
void printGivenLevel(struct node* , int );
int find(struct node*,int );
struct node * Findmin(struct node* );
struct node* del(node*,int );
struct node
{
	int info;
	node *left;
	node *right;
}*root=NULL;
struct node* insert(struct node*temp,int x)
{
	if(temp==NULL)
	{	struct node* newnode;
		newnode=new node;
		newnode->info=x;
		newnode->left=NULL;
		newnode->right=NULL;
		return newnode;
	}
	else
		{
			if(x<(temp->info))
			temp->left=insert(temp->left,x);
			else
			temp->right=insert(temp->right,x);
		}

}

void inorder(struct node* node)
{
	if(node==NULL)
		return;
	inorder(node->left);
	cout << node->info << " ";
	inorder(node->right);
}
void postorder(struct node* node)
{
	if(node==NULL)
		return;
	postorder(node->left);
	postorder(node->right);
	cout << node->info << " ";
}
void preorder(struct node* node)
{
	if(node==NULL)
		return;
	cout << node->info << " ";
	preorder(node->left);
	preorder(node->right);
}
struct node* del(node*temp,int x)
{

	        if(x<temp->info)
		    {
			temp->left=del(temp->left,x);
			return (temp);
		    }
	        else if(x>temp->info)
			{
				temp->right=del(temp->right,x);
				return temp;
			}

			else if(temp->left==NULL && temp->right==NULL)
            {
                delete temp;
                temp=NULL;
                return temp;
            }
            else if(temp->left==NULL)
            {
                struct node*ptr=temp;
                temp=temp->right;
                delete ptr;
                return temp;

            }
            else if(temp->right==NULL)
            {
							struct node*ptr=temp;
							temp=temp->left;
							delete ptr;
							return temp;

            }
            else
            {
							struct node*ptr=Findmin(temp->right);
							temp->info=ptr->info;
							temp->right=del(temp->right,ptr->info);
							return temp;

            }
}
struct node * Findmin(struct node* temp1)
{
    struct node* current = temp1;

    while (current->left != NULL)
        current = current->left;

    return current;
}
int find(struct node*temp,int x)
{
	if(temp==NULL)
		return 0;
	else
	{
		if(temp->info==x)
			return 1;
		else
		{
			if(x<temp->info)
				find(temp->left,x);
			else
				find(temp->right,x);

		}

	}
}
int main()
{
	while(1)
	{	cout << "enter 1 for insertion" << "\n";
		cout <<	"enter 3 for inorder" << "\n";
		cout <<	"enter 4 for postorder" << "\n";
		cout << "enter 5 for preorder" << "\n";
		cout <<	"enter 6 to find" << "\n";
		cout <<	"enter 7 to delete" << "\n";
		int z;
		cout << "enter";
		cin >> z;
		switch(z)
		{
			case 1:	{	int x;
						cout << "enter no u want to insert";
						cin >> x;
						root=insert(root,x);
					}
			break;
            case 3: inorder(root);
			break;
			case 4:postorder(root);
			break;
			case 5:preorder(root);
			break;
			case 6:{	int y;
					cout << "enter no u want to search";
					cin >>y;

					if(find(root,y)==0)
					cout << "Number not found";

					if(find(root,y)==1)
					cout << "found";
					}
			break;
			case 7 :int z;
					cout << "enter no u want to delete";
					root=del(root,z);
			break;
		}
	}
	return 0;
}

