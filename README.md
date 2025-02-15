# Library-Management-system
My first repository in Github 
Author - Om shukla 

#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>
using namespace std;

struct Book {
    string title, author, ISBN;
    bool isAvailable = true;
};

// Vector to store books
vector<Book> library;

// Unordered map for quick book lookup
unordered_map<string, bool> bookStatus;

// Function to add a book
void addBook() {
    Book book;
    cout << "Enter book title: ";
    cin.ignore();
    getline(cin, book.title);
    cout << "Enter author name: ";
    getline(cin, book.author)
    cout << "Enter ISBN: ";
    cin >> book.ISBN;

    library.push_back(book);
    bookStatus[book.title] = true;
    cout << "Book added successfully!\n";
}

// Function to display books
void displayBooks() {
    if (library.empty()) {
        cout << "No books available.\n";
        return;
    }
    cout << "\nLibrary Books:\n";
    for (const auto &book : library) {
        cout << book.title << " by " << book.author 
             << " (ISBN: " << book.ISBN << ") - " 
             << (book.isAvailable ? "Available" : "Borrowed") << endl;
    }
}

// Function to sort books by title
void sortByTitle() {
    sort(library.begin(), library.end(), [](const Book &a, const Book &b) {
        return a.title < b.title;
    });
    cout << "Books sorted by title.\n";
}

// Function to sort books by author
void sortByAuthor() {
    sort(library.begin(), library.end(), [](const Book &a, const Book &b) {
        return a.author < b.author;
    });
    cout << "Books sorted by author.\n";
}

// Function to search for a book by title
void searchBook() {
    cout << "Enter book title to search: ";
    cin.ignore();
    string key;
    getline(cin, key);

    auto it = find_if(library.begin(), library.end(), [&](const Book &b) {
        return b.title == key;
    });

    if (it != library.end()) {
        cout << "Book found: " << it->title << " by " << it->author 
             << " (ISBN: " << it->ISBN << ") - " 
             << (it->isAvailable ? "Available" : "Borrowed") << endl;
    } else {
        cout << "Book not found.\n";
    }
}

// Function to borrow a book
void borrowBook() {
    cout << "Enter book title to borrow: ";
    cin.ignore();
    string key;
    getline(cin, key);

    if (bookStatus.count(key) && bookStatus[key]) {
        bookStatus[key] = false;
        cout << "You borrowed the book: " << key << endl;
    } else {
        cout << "Book not found or already borrowed.\n";
    }
}

// Function to return a book
void returnBook() {
    cout << "Enter book title to return: ";
    cin.ignore();
    string key;
    getline(cin, key);

    if (bookStatus.count(key) && !bookStatus[key]) {
        bookStatus[key] = true;
        cout << "You returned the book: " << key << endl;
    } else {
        cout << "Book not found or not borrowed.\n";
    }
}

// Main Menu
int main() {
    int choice;
    do {
        cout << "\nLibrary Management System\n";
        cout << "1. Add Book\n2. Display Books\n3. Sort by Title\n";
        cout << "4. Sort by Author\n5. Search Book\n6. Borrow Book\n";
        cout << "7. Return Book\n8. Exit\nEnter choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addBook(); break;
            case 2: displayBooks(); break;
            case 3: sortByTitle(); break;
            case 4: sortByAuthor(); break;
            case 5: searchBook(); break;
            case 6: borrowBook(); break;
            case 7: returnBook(); break;
            case 8: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 8);

    return 0;
}
