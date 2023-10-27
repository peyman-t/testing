## Library Management System

### Introduction
Goal: To evaluate students' understanding and practical application of fundamental C++ programming concepts, including program structure, data types, control structures, arrays, pointers, functions, and structures/unions. This summative assessment aims to ensure students can independently develop basic C++ programs that incorporate these essential concepts.

**Learning objectives** 
The assignment tests whether you can:

1. Understand and apply basic C++ programming concepts, such as program structure, data types, variables, expressions, operators, and namespaces.
2. Demonstrate proficiency in using control structures, including if-else statements, loops, and switch-case statements.
3. Develop competence in working with arrays and pointers, including one-dimensional and multi-dimensional arrays, pointer variables, and dynamic memory allocation.
4. Apply functions effectively in C++ programs, including defining and calling functions, recursion, and function overloading.
5. Understand and utilize structures and unions in C++ programs, including defining structures and unions, accessing structure members, and working with nested structures.

### Case/brief/scenario

Scenario: A small library is trying to keep track of their book inventory. The librarian would like to have a simple program to manage the inventory, including adding books, displaying the list of books, and searching for books by title or author.

Assignment: Create a C++ program that helps the librarian manage the book inventory using the following C++ features:

1. Basics of programming: Implement the program structure, data types, variables, expressions, operators, and namespaces as needed.
2. Control structures: Use if-else statements, loops, and switch-case statements to control the flow of the program.
3. Arrays and pointers: Utilize one-dimensional arrays or multi-dimensional arrays and pointer variables to store the book inventory.
4. Functions: Define and call functions to perform various tasks, such as adding books, displaying the list of books, and searching for books by title or author.
5. Structures and unions: Define a structure to represent a book, including details such as title, author, publication year, and ISBN. Optionally, use a union for variable-length data, such as the title or author's name.

## Assignment Details

1. Define a structure to represent a book, including the title, author, publication year, and ISBN.
2. Create an array or dynamic memory allocation to store the book inventory.
3. Implement a function to add books to the inventory:
    
    1. Prompt the user for book details (title, author, publication year, and ISBN).
    2. Store the book details in the book structure.
    3. Add the book to the inventory.
    
4. Implement a function to display the list of books in the inventory:
    
    1. Loop through the inventory and display each book's details.
    
5. Implement a function to search for books by title or author:
    
    1. Prompt the user for a search term (title or author).
    2. Loop through the inventory and display any books that match the search term.
    
6. Implement a menu-driven system using switch-case statements to allow the user to choose between adding books, displaying the list of books, searching for books, or exiting the program.
7. Ensure your code is properly documented with comments and follows the principles of good programming practice.

Upon completion, the librarian should be able to run the program, add books to the inventory, display the list of books, and search for books by title or author.

The Library Management System (LMS) should provide the following functionalities:

1. Book Management:
    1. Add books to the library, including title, author, publication date, ISBN, and genre.
    2. Edit book details, such as updating the title, author, publication date, ISBN, or genre.
    3. Delete books from the library.
    4. Search for books by title, author, publication date, ISBN, or genre.
    5. Display a list of all books in the library.
2. Patron Management:
    1. Register new patrons with relevant information, such as name, address, phone number, and email.
    2. Edit patron details, such as updating name, address, phone number, or email.
    3. Delete patrons from the system.
    4. Search for patrons by name, address, phone number, or email.
    5. Display a list of all registered patrons.
3. Library Staff Management:
    1. Add library staff members with relevant information, such as name, job title, and employee ID.
    2. Edit staff member details, such as updating name, job title, or employee ID.
    3. Delete staff members from the system.
    4. Search for staff members by name, job title, or employee ID.
    5. Display a list of all library staff members.
4. Book Lending and Returning:
    1. Allow patrons to check out books, with the system updating the book's availability status and registering the borrowing patron.
    2. Allow patrons to return books, with the system updating the book's availability status and clearing the borrowing patron's record.
    3. Implement a system to calculate and display overdue fines based on the number of days a book is overdue.
5. Reporting:
    1. Generate reports on the total number of books in the library, broken down by genre.
    2. Generate reports on the total number of patrons and their borrowing history.
    3. Generate reports on the total number of library staff members and their assigned tasks.
6. User Interface:
    1. Design a user-friendly command-line interface (CLI) for staff members to manage books, patrons, and staff.
    2. Implement basic input validation to prevent errors and ensure smooth operation of the system.

### Deliverable

A link to the git repository containing the program.