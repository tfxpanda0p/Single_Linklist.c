// # Single_Linklist.c

//singlelinklist program

#include <stdio.h>
// #include<conio>h>
#include <stdlib.h>

void create();

void addNew();
void addFront();
void addMid();
void addLast();

void rem();
void remFront();
void remMid();
void remLast();

void up();
void upData();
void upIndex();

void display();
void count();

struct node
{
	int data;
	struct node *link;
};

struct node *head;
int co = 0;
main()
{
	int choice;
	// clrscr();
	head = NULL;
	do
	{
		printf("\nMenu:\n1.CREATE \n2.ADDNEW \n3.REMOVE \n4.UPDATE \n5.DISPLAY \n6.COUNT \n7.EXIT \nENTER YOUR CHOICE:- ");
		scanf("%d", &choice);
		switch (choice)
		{
		case 1:
			create();
			break;
		case 2:
			addNew();
			break;
		case 3:
			rem();
			break;
		case 4:
			up();
			break;
		case 5:
			display();
			break;
		case 6:
			count();
			break;
		case 7:
			exit(0);
		default:
			printf("\n WRONG CHOICE,TRY AGAIN \n");
			break;
		}
	} while (1);
}

void create()
{
	if (head == NULL)
	{
		head = (struct node *)malloc(sizeof(struct node));
		printf("\nENTER ANY INTEGER DATA:- ");
		scanf("%d", &head->data);
		head->link = NULL;
	}
	else
	{
		printf("\n LIST ALREADY EXISTS \n");
	}
}

void addNew()
{
	int c;
	if (head != NULL)
	{
		printf("\nSubmenu:\n1.ADD-FRONT \n2.ADD-MID \n3.ADD-LAST \n4.EXIT \nENTER YOUR CHOICE:- ");
		scanf("%d", &c);
		switch (c)
		{
		case 1:
			addFront();
			break;
		case 2:
			addMid();
			break;
		case 3:
			addLast();
			break;
		case 4:
			printf("\n Exiting \n");
			break;
		default:
			printf("\n WRONG CHOICE,TRY AGAIN \n");
		}
	}
	else
	{
		printf("\n FIRST CREATE ONE NODE(By using 'CREATE' option) \n");
	}
}

void addFront()
{
	struct node *head2;
	head2 = (struct node *)malloc(sizeof(struct node));
	printf("\nENTER ANY INTEGER DATA:- ");
	scanf("%d", &head2->data);
	head2->link = head;
	head = head2;
}

void addMid()
{
	int p;
	struct node *temp, *head2;
	if (head->link == NULL)
	{
		printf("\n HERE IS ONLY 1 NODE,FIRST CREATE ATLEAST 2 NODES.{To Access 'ADD-MID'} \n");
	}
	else
	{
		printf("\nENTER THE POSITION:- ");
		scanf("%d", &p);
		count();
		if (p <= co)
		{
			p--;
			temp = head;
			while (p != 1)
			{
				temp = temp->link;
				p--;
			}
			head2 = (struct node *)malloc(sizeof(struct node));
			printf("\nENTER ANY INTGER DATA:- ");
			scanf("%d", &head2->data);
			head2->link = temp->link;
			temp->link = head2;
		}
		else
		{
			printf("\n Invalid Position \n");
		}
	}
}

void addLast()
{
	struct node *head2, *temp;
	temp = head;
	head2 = (struct node *)malloc(sizeof(struct node));
	printf("\nENTER ANY INTEGER DATA:- ");
	scanf("%d", &head2->data);
	head2->link = NULL;
	while (temp->link != NULL)
	{
		temp = temp->link;
	}
	temp->link = head2;
}

void rem()
{
	int c;
	if (head == NULL)
	{
		printf("\n LIST IS EMPTY \n");
	}
	else
	{
		printf("\nSubmenu:\n1.REMOVE-FRONT \n2.REMOVE-MID \n3.REMOVE-LAST \n4.EXIT \nENTER YOUR CHOICE:- ");
		scanf("%d", &c);
		switch (c)
		{
		case 1:
			remFront();
			break;
		case 2:
			remMid();
			break;
		case 3:
			remLast();
			break;
		case 4:
			printf("\n Exiting \n");
			break;
		default:
			printf("\n WRONG CHOICE,TRY AGAIN \n");
		}
	}
}

void remFront()
{
	struct node *temp;
	temp = head;
	head = head->link;
	free(temp);
}

void remMid()
{
	int p;
	struct node *temp = head, *temp2;
	printf("\nENTER THE POSITION:- ");
	scanf("%d", &p);
	p--;
	while (p != 1)
	{
		temp = temp->link;
		p--;
	}
	temp2 = temp->link->link;
	free(temp->link);
	temp->link = temp2;
}

void remLast()
{
	struct node *temp;
	temp = head;
	while (temp->link->link != NULL)
	{
		temp = temp->link;
	}
	free(temp->link);
	temp->link = NULL;
}

void up()
{
	int choice;
	if (head == NULL)
	{
		printf("\n LIST IS EMPTY \n");
	}
	else
	{
		printf("\nSubmenu:\n1.DATA-UPDATE \n2.INDEX-UPDATE \n3.EXIT \nENTER YOUR CHOICE:- ");
		scanf("%d", &choice);
		switch (choice)
		{
		case 1:
			upData();
			break;
		case 2:
			upIndex();
			break;
		case 3:
			printf("\n Exiting \n");
			break;
		default:
			printf("\n WRONG CHOICE,TRY AGAIN \n");
		}
	}
}

void upData()
{
	struct node *temp, *head2;
	int p, u, i;
	temp = head;
	printf("\nENTER THE UPDATE POSITION:- ");
	scanf("%d", &p);
	while (p != 1)
	{
		temp = temp->link;
		p--;
	}
	i = temp->data;
	printf("\nENTER THE UPDATE DATA:- ");
	scanf("%d", &u);
	temp->data = u;
	printf("\n DATA IS UPDATED,%d->%d \n", i, temp->data);
}

void upIndex()
{
	struct node *temp = head, *te = head, *temp3;
	int p1, p2, n;
	printf("\nENTER THE 1ST NODE'S POSITION:- ");
	scanf("%d", &p1);
	printf("\nENTER THE 2ND NODE'S POSITION:- ");
	scanf("%d", &p2);
	while (p1 != 1)
	{
		temp = temp->link;
		p1--;
	}
	while (p2 != 1)
	{
		te = te->link;
		p2--;
	}
	n = temp->data;
	temp->data = te->data;
	te->data = n;
}

void display()
{
	struct node *temp = head;
	if (head == NULL)
	{
		printf("\n LIST IS EMPTY \n");
	}
	else
	{
		printf("\n");
		while (temp != NULL)
		{
			printf("%d\t", temp->data);
			temp = temp->link;
		}
		printf("\n");
	}
}

void count()
{
	struct node *temp = head;
	if (head == NULL)
	{
		co = 0;
	}
	else
	{
		while (temp != NULL)
		{
			co++;
			temp = temp->link;
		}
	}
}
