#include <iostream>
using namespace std;

class Node
{
public:
    int data;
    Node *next;

    Node(int val){
        data = val;
        next = NULL;
    }
};
class LinkedList
{
    Node *head;

public:
    LinkedList(){
        head = NULL;
    }

    void insert_at_beginning(int val){
        Node *newNode = new Node(val);
        newNode->next = head;
        head = newNode;
    }

    bool search(int key){
        Node *temp = head;
        while (temp != NULL)
        {
            if (temp->data == key)
                return true;
            temp = temp->next;
        }
        return false;
    }

    void delete_node(int key)
    {
        if (head == NULL)
            return;

        if (head->data == key){
            Node *toDelete = head;
            head = head->next;
            delete toDelete;
            return;
        }

        Node *temp = head;
        while (temp->next != NULL && temp->next->data != key){
            temp = temp->next;
        }

        if (temp->next == NULL)
            return;

        Node *toDelete = temp->next;
        temp->next = temp->next->next;
        delete toDelete;
    }

    void reverse(){
        Node *prev = NULL;
        Node *curr = head;
        Node *nextNode = NULL;

        while (curr != NULL){
            nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
        }
        head = prev;
    }

    void display()
    {
        Node *temp = head;
        while (temp != NULL){
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }
};

int main()
{
    LinkedList list;
    int choice, value, key;

    do
    {
        cout << "--- Linked List Menu ---" << endl;
        cout << "1. Insert at Beginning" << endl;
        cout << "2. Search" << endl;
        cout << "3. Delete Node" << endl;
        cout << "4. Reverse List" << endl;
        cout << "5. Display List" << endl;
        cout << "6. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            cout << "Enter value to insert: ";
            cin >> value;
            list.insert_at_beginning(value);
            break;
        case 2:
            cout << "Enter value to search: ";
            cin >> key;
            if (list.search(key))
                cout << "Value found!" << endl;
            else
                cout << "Value not found!" << endl;
            break;
        case 3:
            cout << "Enter value to delete: ";
            cin >> key;
            list.delete_node(key);
            break;
        case 4:
            list.reverse();
            break;
        case 5:
            cout << "Current List: ";
            list.display();
            break;
        case 6:
            cout << "Exiting program..." << endl;
            break;
        default:
            cout << "Invalid choice! Try again." << endl;
        }
    } while (choice != 6);

    return 0;
}
