# CIS-277-InfixPostfix
/*
Class: CIS-277-001
Professor: Alan Eliscu
Date: 10/18/2018
Name: Marlen

*/

#include <iostream>
#include <stdlib.h>
#include <string>
#include <cstdio>
#include <cstdlib>
using namespace std;

const int SIZE = 20;
char stck[SIZE];
int top = -1;
char stck2[SIZE];


char pop ()
{
    char data;
    if (top == -1)
        return -1;
    else
    {
        data = stck[top];
        top--;
        return data;
    }
}

void push (char x)
{
    top = top +1;
    stck[top]= x;
}

int priority (char x)
{
    if (x == '(')
        return 0;
    else if (x == '+' || x == '-')
        return 1;
    else if (x == '*' || x == '/')
        return 2;
    else
        return -1;
}

int main ()
{
    char x;
    char xStack[SIZE];
    char *e;
    int i = 0;

    cout<<endl<<"----------------------------"<<endl;
    cout<<endl<<"Infix to Postfix Calculator "<<endl;
    cout<<endl<<"----------------------------\n"<<endl;
    cout << "This program will turn Infix notation to Postfix notation.\n\n";
    cout << "Here are some examples:\n";
    cout << " 1. ((5*4)-(6+4))*(2+8)\n";
    cout << " 2. 2*3+4\n";
    cout << " 3. (2+3)*10\n\n";
    cout << " As you can see spaces in between operators and operands must not be input into this program.\n\n";

    cout << "Now please enter an equation you'd like to convert. (Max: 20 characters)\n";
    cout << "Enter: ";
    cin >> xStack;
    e = xStack;

    cout << "\n\nPostfix Notaion: ";

    while (*e != '\0')
    {
        if (isalnum(*e))
            cout << *e << " ";
        else if (*e == '(')
            push(*e);
        else if (*e == ')')
        {
            while ( (x=pop()) != '(')
                cout << x << " ";
        }
        else
        {
            while (priority(stck[top]) >= priority(*e))
                cout << pop() << " ";
                push (*e);
        }

        e++;
    }

    while (top != -1)
    {
        cout << pop() << " ";
    }

    cout << endl << endl;

    system("pause");
    return 0;
}

