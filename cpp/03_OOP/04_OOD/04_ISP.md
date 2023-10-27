### Interface Segregation Principle (ISP)
The Interface Segregation Principle (ISP) is one of the SOLID principles in object-oriented programming that advocates for designing small, cohesive interfaces rather than large and monolithic ones. This principle encourages the creation of interfaces that are tailored to specific needs and only expose the functionality that is relevant to the client.

In C++, the concept of ISP can be applied using abstract classes or pure virtual functions. An abstract class is a class that has at least one pure virtual function, which means that the class cannot be instantiated on its own, but can be used as a base class for other classes. Pure virtual functions are defined using the virtual keyword followed by = 0 in their declaration.

An example of applying ISP in C++ would be to create an abstract class `IAnimal` that defines only the methods that are necessary for working with animals in general, such as `eat()` and `sleep()`. Then, we can create more specialized interfaces, such as `IMammal`, `IBird`, and `IReptile`, each with their own methods that are specific to those types of animals. These specialized interfaces can inherit from `IAnimal` and add their own methods as needed.

Here's an example code that demonstrates this:
```cpp
#include <iostream>

class Machine {
public:
    virtual void print() = 0;
    virtual void fax() = 0;
    virtual void scan() = 0;
};

class AllInOnePrinter : public Machine {
public:
    void print() override {
        std::cout << "Printing..." << std::endl;
    }
    void fax() override {
        std::cout << "Sending a fax..." << std::endl;
    }
    void scan() override {
        std::cout << "Scanning a document..." << std::endl;
    }
};

class OldFashionedPrinter : public Machine {
public:
    void print() override {
        std::cout << "Printing..." << std::endl;
    }
    void fax() override {
        std::cout << "Sorry, I can't fax." << std::endl;
    }
    void scan() override {
        std::cout << "Sorry, I can't scan." << std::endl;
    }
};

int main() {
    AllInOnePrinter allInOnePrinter;
    OldFashionedPrinter oldFashionedPrinter;

    allInOnePrinter.print();
    allInOnePrinter.fax();
    allInOnePrinter.scan();

    oldFashionedPrinter.print();
    oldFashionedPrinter.fax();
    oldFashionedPrinter.scan();

    return 0;
}
```
This code does not adhere to ISP because the interface `IMachine` is too large and clients of the interface are forced to implement methods that they don't need. This violates the principle that clients should not be forced to depend on methods that they do not use.

Now, let's fix the above code:
```cpp
#include <iostream>

class Printer {
public:
    virtual void print() = 0;
};

class Scanner {
public:
    virtual void scan() = 0;
};

class Fax {
public:
    virtual void fax() = 0;
};

class AllInOnePrinter : public Printer, public Scanner, public Fax {
public:
    void print() override {
        std::cout << "Printing..." << std::endl;
    }
    void fax() override {
        std::cout << "Sending a fax..." << std::endl;
    }
    void scan() override {
        std::cout << "Scanning a document..." << std::endl;
    }
};

class OldFashionedPrinter : public Printer {
public:
    void print() override {
        std::cout << "Printing..." << std::endl;
    }
};

int main() {
    AllInOnePrinter allInOnePrinter;
    OldFashionedPrinter oldFashionedPrinter;

    allInOnePrinter.print();
    allInOnePrinter.fax();
    allInOnePrinter.scan();

    oldFashionedPrinter.print();

    return 0;
}
```
This code adheres to ISP because the `IMachine` interface has been broken down into smaller, more specific interfaces (`IPrinter`, `IScanner`, and `IFax`) so that clients can depend on only the methods that they need. This makes the code more modular and flexible.

Consequences of violating ISP can lead to the creation of interfaces that are too large and complex, which can make them difficult to use and maintain. Additionally, changes made to the interface can have a ripple effect on all the classes that depend on it, which can make it harder to evolve the system over time.