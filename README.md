# -Student-Details-Management-System-Using-Singly-Linked-List-in-C-Programming-Language
This project is developed using C++ programming language with the concept of Data Structures. It is used to store and manage student details such as Roll Number, Name and Mark.The program uses a Singly Linked List to store student records dynamically. Each node contains student information and a pointer to the next node.#include <iostream>
#include <string>
using namespace std;

struct node
{
    int rollno;
    string name;
    float mark;
    struct node *next;
};

struct node *first = NULL;
struct node *last = NULL;

class linked_list
{
public:
    void insert_begin(int, string, float);
    void insert_end(int, string, float);
    void deletion(int);
    void print();
};

void linked_list::insert_begin(int r, string n, float m)
{
    struct node *ptr = new node;

    ptr->rollno = r;
    ptr->name = n;
    ptr->mark = m;
    ptr->next = first;

    first = ptr;

    if (last == NULL)
        last = ptr;

    cout << "Student inserted successfully\n";
}

void linked_list::insert_end(int r, string n, float m)
{
    struct node *ptr = new node;

    ptr->rollno = r;
    ptr->name = n;
    ptr->mark = m;
    ptr->next = NULL;

    if (first == NULL)
    {
        first = last = ptr;
    }
    else
    {
        last->next = ptr;
        last = ptr;
    }

    cout << "Student inserted successfully\n";
}

void linked_list::deletion(int r)
{
    struct node *temp = first;
    struct node *prev = NULL;

    while (temp != NULL && temp->rollno != r)
    {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL)
    {
        cout << "Student not found\n";
        return;
    }

    if (prev == NULL)
        first = temp->next;
    else
        prev->next = temp->next;

    if (temp == last)
        last = prev;

    delete temp;

    cout << "Student deleted successfully\n";
}

void linked_list::print()
{
    struct node *temp = first;

    if (first == NULL)
    {
        cout << "No student records available\n";
        return;
    }

    cout << "\nStudent Details:\n";

    while (temp != NULL)
    {
        cout << "\nRoll Number: " << temp->rollno;
        cout << "\nName: " << temp->name;
        cout << "\nMark: " << temp->mark << endl;

        temp = temp->next;
    }
}

int main()
{
    linked_list l;
    int choice, r;
    string n;
    float m;

    do
    {
        cout << "\n--- STUDENT DETAILS MANAGEMENT ---";
        cout << "\n1. Insert at Beginning";
        cout << "\n2. Insert at End";
        cout << "\n3. Delete Student";
        cout << "\n4. Display Students";
        cout << "\n5. Exit";

        cout << "\nEnter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            cout << "Enter Roll Number: ";
            cin >> r;
            cout << "Enter Name: ";
            cin >> n;
            cout << "Enter Mark: ";
            cin >> m;
            l.insert_begin(r, n, m);
            break;

        case 2:
            cout << "Enter Roll Number: ";
            cin >> r;
            cout << "Enter Name: ";
            cin >> n;
            cout << "Enter Mark: ";
            cin >> m;
            l.insert_end(r, n, m);
            break;

        case 3:
            cout << "Enter Roll Number to Delete: ";
            cin >> r;
            l.deletion(r);
            break;

        case 4:
            l.print();
            break;

        case 5:
            cout << "Program Exited";
            break;

        default:
            cout << "Invalid Choice";
        }

    } while (choice != 5);

    return 0;
}
