# Library-Management-System
#include <iostream>
#include <vector>
using namespace std;

class MediaItem {
protected:
    int id;
    string title;
    bool issued;

public:
    MediaItem(int i, string t) {
        id = i;
        title = t;
        issued = false;
    }

    virtual void display() = 0;

    void issue() {
        if (!issued) {
            issued = true;
            cout << "Item Issued Successfully!\n";
        } else {
            cout << "Item Already Issued!\n";
        }
    }

    void returnItem() {
        if (issued) {
            issued = false;
            cout << "Item Returned Successfully!\n";
        } else {
            cout << "Item was not Issued.\n";
        }
    }

    int getId() {
        return id;
    }

    bool isIssued() {
        return issued;
    }
};

class Book : public MediaItem {
    string author;

public:
    Book(int i, string t, string a)
        : MediaItem(i, t) {
        author = a;
    }

    void display() override {
        cout << "\nBook ID : " << id;
        cout << "\nTitle   : " << title;
        cout << "\nAuthor  : " << author;
        cout << "\nStatus  : " << (issued ? "Issued" : "Available") << endl;
    }
};

class Journal : public MediaItem {
    string publisher;

public:
    Journal(int i, string t, string p)
        : MediaItem(i, t) {
        publisher = p;
    }

    void display() override {
        cout << "\nJournal ID : " << id;
        cout << "\nTitle      : " << title;
        cout << "\nPublisher  : " << publisher;
        cout << "\nStatus     : " << (issued ? "Issued" : "Available") << endl;
    }
};

int main() {

    vector<MediaItem*> library;

    library.push_back(new Book(101,"C++ Programming","Bjarne Stroustrup"));
    library.push_back(new Journal(201,"IEEE Journal","IEEE"));

    int choice,id;

    do {

        cout<<"\n===== LIBRARY MANAGEMENT SYSTEM =====\n";
        cout<<"1. View Library\n";
        cout<<"2. Issue Item\n";
        cout<<"3. Return Item\n";
        cout<<"4. Exit\n";
        cout<<"Enter Choice: ";
        cin>>choice;

        switch(choice){

        case 1:

            for(auto item:library)
                item->display();

            break;

        case 2:

            cout<<"Enter Item ID: ";
            cin>>id;

            for(auto item:library)
                if(item->getId()==id)
                    item->issue();

            break;

        case 3:

            cout<<"Enter Item ID: ";
            cin>>id;

            for(auto item:library)
                if(item->getId()==id)
                    item->returnItem();

            break;

        case 4:

            cout<<"\nThank You!\n";
            break;

        default:

            cout<<"Invalid Choice!\n";
        }

    }while(choice!=4);

    for(auto item:library)
        delete item;

    return 0;
}
