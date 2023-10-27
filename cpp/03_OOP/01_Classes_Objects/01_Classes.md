## Classes
Classes are user-defined data types that allow for encapsulation of data and functionality into a single entity. Objects are instances of classes, meaning they are created from the class definition and hold their own copy of the class data.

The relationship between classes and objects is one of a template and its instantiations. A class provides a blueprint for creating objects, and objects are the actual instances created from that blueprint. In other words, a class defines the data and functions that an object will have, and an object is the specific instance of that class that has been created.

Basic class syntax and structure include the use of access specifiers (public, private, and protected) to define the visibility and accessibility of class members, such as data and functions. The structure of a class typically includes a constructor and destructor to handle object creation and destruction, as well as member functions to define the behavior of the class.

The basic syntax for declaring a class in C++ is as follows:
```cpp
class ClassName {
    // Access specifier
    private:
        // Data members
        int member1;
        float member2;
        char member3;

    // Access specifier
    public:
        // Member functions
        void function1();
        int function2(float arg);
};
```
Here, `ClassName` is the name of the class, and it contains data members and member functions. The data members are declared inside the class and represent the attributes or properties of the objects. The member functions are also declared inside the class and provide the operations that can be performed on the objects.

There are three access specifiers in C++: `private`, `public`, and `protected`. They determine the level of access that the data members and member functions have. `private` data members and member functions can only be accessed by other members of the same class, while `public` data members and member functions can be accessed by any part of the program. `protected` data members and member functions are similar to `private`, but they can also be accessed by derived classes; we will discuss this in the next lesson after learning inheritance.

Here is an example of a simple class definition in C++:
```cpp
class Rectangle {
    private:
        int width;
        int height;
    public:
        Rectangle(int w, int h) {
            width = w;
            height = h;
        }
        int area() {
            return width * height;
        }
};
```
In this example, the `Rectangle` class is defined with two private member variables `width` and `height`, and two public member functions: a constructor that takes two integer arguments to set the `width` and `height`, and an `area()` function that returns the area of the rectangle. The `private` access specifier means that the data members are only accessible within the class, while the `public` access specifier means that the member functions can be called from outside the class.

To create an object of this class, we can use the following code:
```cpp
Rectangle rect(4, 5);
int area = rect.area();
```
In this code, we create a `Rectangle` object called `rect` with a width of 4 and a height of 5. We then call the `area()` function on rect to calculate and store the area in the area variable.

Here is another example of a class definition:
```cpp
class Person {
private:
    std::string name;
    int age;

public:
    void setName(std::string n) {
        name = n;
    }

    std::string getName() {
        return name;
    }

    void setAge(int a) {
        age = a;
    }

    int getAge() {
        return age;
    }
};
```
In this example, we have defined a class `Person` with two private member variables, `name` and `age`. We have also declared four public member functions: `setName`, `getName`, `setAge`, and `getAge`. The `setName` and `setAge` methods are used to set the values of the `name` and `age` member variables, while the `getName` and `getAge` methods are used to retrieve their values.

Note that we have used access specifiers such as `private` and `public` to control the accessibility of the member variables and member functions. `private` variables and functions can only be accessed by other member functions of the same class, while `public` variables and functions can be accessed by any code that has access to an instance of the class.

We can create an object of the class `Person` by declaring a variable of type `Person`:
```cpp
Person p;
```
Once we have created an object, we can access its member variables and member functions using the dot operator:
```cpp
p.setName("John");
p.setAge(30);
std::cout << p.getName() << " is " << p.getAge() << " years old." << std::endl;
```
This will output `"John is 30 years old."`

### Class Instantiation and Constructors
In C++, objects are instances of classes that are created using constructors. Constructors are special member functions that are used to initialize the objects of a class. Constructors are called automatically when an object is created and are used to initialize the member variables of the object. They have the same name as the class and no return type.

* Default constructors are constructors that take no arguments. They are used to create an object with default values for its member variables. If a class does not define any constructors, then the compiler automatically generates a default constructor.

* Parameterized constructors are constructors that take one or more arguments. They are used to initialize the member variables of the object with the values passed as arguments. In the example below, the `Person` class has a parameterized constructor that takes three arguments (`name`, `age`, and `height`) and initializes the corresponding member variables.

* Constructor overloading is the practice of defining multiple constructors with different sets of parameters. This allows objects to be created with different initial values, depending on the arguments passed to the constructor.

* Member initializer lists were introduced in C++11 and provide a more efficient way to initialize the member variables of a class. Instead of initializing the variables inside the constructor body, they can be initialized in the constructor declaration using an initializer list.

* Delegating constructors were also introduced in C++11 and allow constructors to call other constructors of the same class. This can help to reduce code duplication and make constructors more flexible.

Here's an example that demonstrates the use of constructors in a class:
```cpp
#include <iostream>
#include <string>

class Person {
public:
    std::string name;
    int age;
    float height;

    // Default constructor
    Person() {
        name = "Unknown";
        age = 0;
        height = 0.0;
    }

    // Parameterized constructor
    Person(std::string n, int a, float h) {
        name = n;
        age = a;
        height = h;
    }

    // Constructor overloading
    Person(std::string n) {
        name = n;
        age = 0;
        height = 0.0;
    }

    // Member initializer list constructor
    Person(std::string n, int a) : name(n), age(a), height(0.0) {}

    // Delegating constructor
    Person(float h) : Person("Unknown", 0, h) {}

    void printInfo() {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Age: " << age << std::endl;
        std::cout << "Height: " << height << "m" << std::endl;
    }
};

int main() {
    Person p1; // Default constructor
    p1.printInfo();

    Person p2("John Doe", 30, 1.75); // Parameterized constructor
    p2.printInfo();

    Person p3("Jane Smith"); // Constructor overloading
    p3.printInfo();

    Person p4("Bob Williams", 25); // Member initializer list constructor
    p4.printInfo();

    Person p5(1.8); // Delegating constructor
    p5.printInfo();

    return 0;
}
```
The above example is a class called `Person` that has three member variables: `name`, `age`, and `height`. It also has a constructor that takes in three arguments: a `string` for the `name`, an `int` for the `age`, and a `float` for the `height`. The constructor sets the member variables to the values passed in as arguments.

The constructor in this example is a parameterized constructor because it takes in arguments. It is not a default constructor because it doesn't have any default values for the arguments.

Here's an example of how you would create an object of the Person class using this constructor:
```cpp
Person p1("John Doe", 30, 1.8);
```
This creates a `Person` object called `p1` with the name "John Doe", age 30, and height 1.8.

In addition to parameterized constructors, you can also have default constructors, which are constructors that don't take any arguments. Here's an example of a default constructor for the `Person` class:
```cpp
Person() {
    name = "";
    age = 0;
    height = 0;
}
```
This default constructor sets all the member variables to default values. You can create an object of the `Person` class using this default constructor like this:
```cpp
Person p2;
```
This creates a `Person` object called `p2` with default values for all the member variables.

You can also have constructor overloading, which is when you have multiple constructors with different parameter lists. This allows you to create objects of the same class using different sets of arguments. Here's an example of constructor overloading for the `Person` class:
```cpp
Person(std::string n) {
    name = n;
    age = 0;
    height = 0;
}

Person(std::string n, int a) {
    name = n;
    age = a;
    height = 0;
}
```
These constructors allow you to create a `Person` object with just a `name`, or with a `name` and an `age`, without having to provide a `height`.

Finally, C++11 introduced member initializer lists, which allow you to initialize the member variables of a class directly in the constructor declaration. Here's an example of using a member initializer list in the `Person` class:
```cpp
Person(std::string n, int a, float h)
    : name(n), age(a), height(h) {
}
```
This constructor sets the member variables to the values passed in as arguments using a member initializer list, rather than setting them in the constructor body.

C++11 also introduced delegating constructors, which allow you to call one constructor from another constructor in the same class. This can be useful when you have multiple constructors that share common code. Here's an example of a delegating constructor for the `Person` class:
```cpp
Person() : Person("", 0, 0) {}

Person(std::string n, int a) : Person(n, a, 0) {}
```
These constructors delegate to the parameterized constructor with default values for the height. The first constructor delegates to the second constructor with empty string and zero values for age and height, and the second constructor delegates to the parameterized constructor with a height of 0.

### Destructors
In C++, destructors are special member functions that are called when an object of a class is destroyed or goes out of scope. The main purpose of destructors is to perform any cleanup or resource management needed before the object is destroyed, such as releasing memory or closing files.

A destructor has the same name as the class, preceded by a tilde (~), and no parameters. It is defined with the syntax:
```cpp
class MyClass {
public:
    // Constructor
    MyClass();

    // Destructor
    ~MyClass();
};
```
Destructors are called automatically by the compiler when an object is destroyed, so you don't need to explicitly call them. They can also be explicitly called, but it is usually not recommended.

Here's an example of a class with a destructor that deallocates memory:
```cpp
class MyClass {
public:
    // Constructor
    MyClass() {
        data = new int[10];
    }

    // Destructor
    ~MyClass() {
        delete[] data;
    }

private:
    int* data;
};
```
In this example, the constructor allocates memory for an array of integers, and the destructor deallocates the memory when the object is destroyed. This ensures that the memory is released properly and prevents memory leaks.

> **Note**
>
> It's important to note that if you don't define a destructor explicitly, the compiler will generate a default destructor that does nothing. However, if your class contains dynamically allocated memory or other resources that need to be cleaned up, you should define a destructor to ensure proper cleanup.

For the `Person` class defined before, we can declare a destructor:
```cpp
class Person {
public:
    // All other parts

    // ...

    // Destructor
    ~Person() {
        std::cout << "Destructor called for " << name << std::endl;
    }
};
```
In this example, the destructor is defined using the tilde (`~`) followed by the class name, and it is implemented to print a message indicating that the destructor has been called for the specific `Person` object being destroyed. This can be useful for tracking the lifetime of objects and ensuring that any resources they were using are properly released.

## `friend`
The `friend` keyword in C++ allows a non-member function or class to access the private or protected members of a class. This can be useful in certain situations, but should be used with caution, as it can break encapsulation and increase code complexity.

Here is an example of a class with different access modifiers and the friend keyword:
```cpp
#include <iostream>


class BankAccount {
private:
    std::string ownerName;
    double balance;
    
    // Private member function
    void updateBalance(double amount) {
        balance += amount;
    }

public:
    // Public member function
    void deposit(double amount) {
        updateBalance(amount);
    }

    // Public member function
    double getBalance() const {
        return balance;
    }

    // Friend function
    friend void transfer(BankAccount& from, BankAccount& to, double amount);
};

// Friend function definition
void transfer(BankAccount& from, BankAccount& to, double amount) {
    from.updateBalance(-amount);
    to.updateBalance(amount);
}


int main() {
    BankAccount b1, b2;
    transfer(b1, b2, 2);

    std::cout << b1.getBalance() << std::endl;
    return 0;
}
```
In this example, the `ownerName` and `balance` member variables are declared as `private`, while the `deposit()` and `getBalance()` member functions are declared as `public`. The `updateBalance()` member function is also declared as `private`, and is called by the `deposit()` function.

The `transfer()` function is declared as a friend of the `BankAccount` class, allowing it to access the private `updateBalance()` function of `BankAccount`. This function can be used to transfer money between two bank accounts.

## Types of Member Functions
In C++, member functions are functions that are defined inside a class and can access the class's data members and other member functions. They are used to implement the behavior of a class and allow objects to perform actions and manipulate their own data. Member functions can be defined and implemented inside the class definition or outside of it, and can be declared as inline to improve performance.

In addition, member functions can be declared as `const`, which means that they do not modify the object's state. This is particularly useful for read-only functions that do not need to modify the object's data members.

Static member functions are member functions that belong to the class itself rather than individual objects. They can be called using the class name and the scope resolution operator, without the need for an object instance. They are useful for implementing class-level functionality or operations that do not depend on object state.

Here is an example that demonstrates the use of member functions in a C++ class:
```cpp
#include <iostream>

class Rectangle {
private:
    int width;
    int height;

public:
    Rectangle(int w, int h) : width(w), height(h) {}

    int area() const {
        return width * height;
    }

    void resize(int w, int h) {
        width = w;
        height = h;
    }

    static int maxArea(const Rectangle& r1, const Rectangle& r2) {
        return std::max(r1.area(), r2.area());
    }
};

int main() {
    Rectangle r(3, 4);
    std::cout << "Area: " << r.area() << std::endl;

    r.resize(5, 6);
    std::cout << "Area after resize: " << r.area() << std::endl;

    Rectangle r1(2, 3);
    Rectangle r2(4, 5);
    std::cout << "Maximum area: " << Rectangle::maxArea(r1, r2) << std::endl;

    return 0;
}
```
In this example, the `Rectangle` class has member functions `area`, `resize`, and `maxArea`. The `area` function returns the area of the rectangle object, while the `resize` function modifies its `width` and `height` data members. The `maxArea` function is a `static` member function that takes two `Rectangle` objects as arguments and returns the maximum area between them.

In the above example, the `area()` function is defined as `const` member function. This means that it is a read-only function and cannot modify any data members of the class. It is good practice to declare member functions const when they do not modify the class state.

On the other hand, the `maxArea()` function is defined as a `static` member function. This means that it is not tied to any particular instance of the class, and can be called using the class name itself, rather than an object of the class. Static member functions do not have access to non-static data members of the class, and they can only access static data members.

In the `maxArea()` function, `const` reference parameters are used to pass the `Rectangle` objects to avoid unnecessary copying of the objects. This is an efficient way of passing objects to functions.

## Static Data Members
Static data members are class variables that are shared among all instances of the class. These variables are declared with the keyword "static" and are defined outside the class definition.

Here's an example of a class with a static data member:
```cpp
#include <iostream>

class MyClass {
public:
    static int count; // declaration of static data member

    MyClass() { count++; } // constructor that increments count

    void printCount() { std::cout << "Count: " << count << std::endl; }
};

int MyClass::count = 0; // definition and initialization of static data member

int main() {
    MyClass obj1, obj2, obj3;
    obj1.printCount(); // prints "Count: 3"
    obj2.printCount(); // prints "Count: 3"
    obj3.printCount(); // prints "Count: 3"
    
    std::cout << MyClass::count << std::endl; // prints "3"
    
    return 0;
}
```
In this example, the static data member `count` is initialized to zero outside the class definition. When objects of the class are created, the constructor increments the count, so all objects share the same value of `count`.

Static data members can be accessed using the scope resolution operator (`::`) outside the class definition. For example, `MyClass::count` returns the value of the static data member `count`.

> **Note**
>
> Use cases for static data members include counting the number of instances of a class, storing shared data among all instances of a class, and providing global data that can be accessed from anywhere in the program.

## Pointers to Classes
Once an object is created, you can access its data members and member functions using the dot operator (`.`) for objects and the arrow operator (`->`) for pointers to objects. For example, to access the `age` of `p1`, you can write:
```cpp
Person p1;
std::cout << p1.age << std::endl;
```
If you have a pointer to an object, you can access its members using the arrow operator (`->`). For example, if you have a pointer `p2` to `p1`, you can access its `age` using:
```cpp
Person *p2 = &p1;
std::cout << p2->age << std::endl;
```
Note that you must use the `->` operator when accessing members through a pointer to an object, even if the member you are accessing is not a pointer.

## Operator Overloading
Operator overloading in C++ allows classes to define their own behavior for certain operators when used with objects of that class. This provides a way to make classes behave more like built-in types, and allows for more natural and intuitive code.

Some common operators that can be overloaded include arithmetic operators such as `+`, `-`, `*`, `/`, comparison operators such as `==`, `!=`, `<`, `>`, and assignment operators such as `=`. Additionally, stream insertion and extraction operators `<<` and `>>` can be overloaded to allow objects to be input and output from streams.

Unary operators such as `++` and `--` can also be overloaded to provide custom behavior for incrementing and decrementing objects of a class.

Here is an example of overloading the addition operator for a class:
```cpp
class Vector {
public:
    int x, y, z;
    Vector operator+(const Vector& other) const {
        return { x + other.x, y + other.y, z + other.z };
    }
};

int main() {
    Vector v1 { 1, 2, 3 };
    Vector v2 { 4, 5, 6 };
    Vector v3 = v1 + v2;
    std::cout << v3.x << ", " << v3.y << ", " << v3.z << std::endl; // Output: 5, 7, 9
    return 0;
}
```
The above code defines a class called `Vector` with three integer data members (`x`, `y`, and `z`). The class also overloads the `+` operator using the `operator+` function, which takes a `const` reference to another `Vector` object and returns a new `Vector` object whose data members are the sum of the corresponding data members of the two vectors. In the main function, two Vector objects (`v1` and `v2`) are initialized with values (1, 2, 3) and (4, 5, 6), respectively. These vectors are added using the overloaded `+` operator, and the result is stored in `v3`. Finally, the `x`, `y`, and `z` values of `v3` are printed to the console, which should output "5, 7, 9". This code demonstrates how operator overloading can be used to define custom behavior for built-in operators on user-defined types.

here are some more examples of operator overloading in C++ classes:
Overloading the comparison operator:
```cpp
#include <iostream>

class Fraction {
public:
    int numerator;
    int denominator;

    bool operator==(const Fraction& other) const {
        return numerator / denominator == other.numerator / other.denominator;
    }
};

int main() {
    Fraction f1 { 1, 2 };
    Fraction f2 { 2, 4 };
    if (f1 == f2) {
        std::cout << "The fractions are equal" << std::endl;
    }
    return 0;
}
```
The above code defines a `Fraction` class with two integer data members, `numerator` and `denominator`. It overloads the `==` operator to check whether two fractions are equal by comparing their decimal values. If the decimal value of the first fraction (`numerator/denominator`) is equal to the decimal value of the second fraction (`other.numerator/other.denominator`), then the operator returns true.

In the `main` function, two `Fraction` objects are created with different values but equivalent fractions (`f1` is `1/2` and `f2` is `2/4`, which is equivalent to `1/2`). The `==` operator is then used to check if they are equal, and since they are, the program outputs `"The fractions are equal"`.

Overloading the assignment operator:
```cpp
#include <iostream>

class Person {
public:
    std::string name;
    int age;

    Person& operator=(const Person& other) {
        name = other.name;
        age = other.age;
        return *this;
    }
};

int main() {
    Person p1 { "Alice", 20 };
    Person p2 { "Bob", 22 };
    p1 = p2;
    std::cout << p1.name << ", " << p1.age << std::endl; // Output: "Bob, 22"
    return 0;
}
```
The above code defines a class `Person` that has two data members, `name` and `age`. The class also defines an overloaded assignment operator, `operator=`, which takes a `const` reference to another `Person` object and returns a reference to the object being assigned to.

In the `main` function, two `Person` objects `p1` and `p2` are defined and initialized with `name` and `age`. Then, `p2` is assigned to `p1` using the overloaded assignment operator. This assigns the value of `p2` to `p1`. Finally, the `name` and `age` of `p1` are printed to the console using the `std::cout` statement.

The overloaded `operator=` copies the `name` and `age` of the other object to the current object (`this`) and returns a reference to the current object. This allows the assignment to be chained, i.e., `p1 = p2 = p3`, where `p3` is another `Person` object. The assignment operator is useful when objects need to be copied or assigned to each other in a clean and efficient way.

Overloading the stream insertion operator:
```cpp
#include <iostream>

class Date {
public:
    int day;
    int month;
    int year;

    friend std::ostream& operator<<(std::ostream& os, const Date& date) {
        os << date.day << "/" << date.month << "/" << date.year;
        return os;
    }
};

int main() {
    Date d { 29, 3, 2023 };
    std::cout << "Today's date is: " << d << std::endl; // Output: "Today's date is: 29/3/2023"
    return 0;
}
```
The above code defines a `Date` class with three int data members `day`, `month`, and `year`. It also overloads the `<<` operator using the `friend` keyword, which allows the operator to access private members of the `Date` class. The overloaded `<<` operator takes an `std::ostream` object `os` and a `const Date&` object date, and returns an `std::ostream` object. It then inserts the values of `date.day`, `date.month`, and `date.year` into the `os` stream, separated by forward slashes (`/`). In the `main()` function, a `Date` object `d` is created with values 29, 3, and 2023 for `day`, `month`, and `year`, respectively. The overloaded `<<` operator is then used to insert `d` into the output stream, resulting in the string `"Today's date is: 29/3/2023"`.

## Encapsulation
Encapsulation is the practice of hiding the internal details of an object from the outside world and providing a public interface to access or modify its state. In C++, this is usually achieved by declaring data members as private and providing public member functions to access or modify them. Encapsulation helps to ensure data integrity, enhances security, and enables easier maintenance and modification of code.

To follow the best practices of encapsulation in C++, it is important to minimize direct access to private data members and instead provide access through public member functions. This allows for greater control over how data is accessed and modified, and helps to prevent unintended changes to the object's state. Additionally, it is important to ensure that public functions properly validate any input parameters and enforce any necessary constraints on the object's state to maintain its integrity.

Finally, it is also a good practice to provide constructors and destructors to properly initialize and clean up object state, respectively. Constructors should be used to ensure that an object is properly initialized to a valid state, while destructors should be used to clean up any resources used by the object.

Overall, encapsulation is an important design principle in C++ that helps to ensure the integrity and maintainability of code. By providing a well-defined public interface to access and modify object state, encapsulation helps to minimize the risk of unintended changes and improve code quality.