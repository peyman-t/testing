## Introduction to Polymorphism
Polymorphism is the ability of objects of different classes to be treated as if they are objects of the same class. It is a powerful concept in object-oriented programming that allows you to write flexible and reusable code. Polymorphism is an important part of C++ programming, and it has several benefits, including code reusability, extensibility, and abstraction.

### Definition of Polymorphism
Polymorphism is a Greek word that means "many forms." In programming, polymorphism refers to the ability of objects to take on different forms. In C++, polymorphism is achieved through function overloading and virtual functions.

### Benefits of using Polymorphism
Polymorphism has several benefits in C++ programming, including code reusability, extensibility, and abstraction. By using polymorphism, you can write code that is more flexible, easier to maintain, and easier to understand. Polymorphism also makes it possible to write code that is more reusable, which can save time and effort in the long run.

### Static (compile-time) and Dynamic (runtime) Polymorphism
C++ supports two types of polymorphism: static (compile-time) and dynamic (runtime). Static polymorphism is achieved through function overloading and template functions, while dynamic polymorphism is achieved through virtual functions and inheritance.

Static polymorphism is resolved at compile-time, which means that the compiler selects the appropriate function to call based on the arguments passed to it. In contrast, dynamic polymorphism is resolved at runtime, which means that the appropriate function is selected based on the type of the object that the function is called on.

An example of static polymorphism is function overloading. Function overloading allows you to define multiple functions with the same name, but different argument lists. The compiler selects the appropriate function to call based on the type of the arguments passed to it.

An example of dynamic polymorphism is function overriding and virtual functions. Virtual functions are functions that are declared in a base class and can be overridden in a derived class. The appropriate function is selected based on the type of the object that the function is called on. In the following, we will introduce these concepts in more details.

### Function Overloading
Function overloading allows us to define multiple functions with the same name but with different parameters. The compiler distinguishes between the functions based on the number, type, and order of the arguments passed to them. This feature is especially useful when we need to perform similar operations on different data types.

Example:
```cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
};
```
In this example, we have two overloaded functions called `add`. One function adds two integers, and the other function adds two doubles.

### Function Overriding
Function overriding is the process of redefining a base class function in a derived class with the same signature (name and parameters). When a function is overridden, the function in the derived class replaces the function in the base class, and the derived class function is called when the function is invoked on an object of the derived class.

#### Virtual Functions
Virtual functions in C++ allow a function to be overridden in a derived class, enabling dynamic binding or late binding of function calls. This allows the program to determine which function to call at runtime based on the type of object being referred to, rather than at compile time.

Here's an example of using virtual functions in C++:
```cpp
#include <iostream>

class Animal {
public:
    virtual void makeSound() {
        std::cout << "The animal makes a generic sound." << std::endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "The dog barks." << std::endl;
    }
};

class Cat : public Animal {
public:
    void makeSound() override {
        std::cout << "The cat meows." << std::endl;
    }
};

int main() {
    Animal *animal1 = new Animal();
    Animal *animal2 = new Dog();
    Animal *animal3 = new Cat();

    animal1->makeSound();
    animal2->makeSound();
    animal3->makeSound();

    delete animal1;
    delete animal2;
    delete animal3;

    return 0;
}
```
In this example, we have a base class called `Animal` with a virtual function called `makeSound()`. We also have two derived classes, `Dog` and `Cat`, which override `makeSound()` with their own specific implementations.

In the `main()` function, we create three `Animal` pointers, `animal1`, `animal2`, and `animal3`. We initialize `animal2` and `animal3` with pointers to `Dog` and `Cat` objects, respectively. When we call `makeSound()` on each of these pointers, the program will determine which implementation of `makeSound()` to use based on the actual type of the object being referred to (i.e. dynamic binding). So, `animal2->makeSound()` will call the `Dog` implementation of `makeSound()`, while `animal3->makeSound()` will call the `Cat` implementation.

The `override` keyword is used to explicitly indicate that a virtual function is intended to override a function with the same name in the base class. This is useful for detecting errors at compile time when the function signatures do not match.

#### Pure Virtual Functions and Abstract Classes
A pure virtual function is a virtual function that is declared in the base class but has no implementation. An abstract class is a class that contains at least one pure virtual function and cannot be instantiated. Any class that inherits from an abstract class must implement all of its pure virtual functions, or else it will also be considered an abstract class.

Example:
```cpp
class Shape {
public:
    virtual double area() = 0; // Pure virtual function
};

class Circle : public Shape {
public:
    double area() override {
        return 3.14 * radius * radius;
    }
private:
    double radius;
};
```
In this example, we have a base class `Shape` that has a pure virtual function `area()`. The derived class `Circle` inherits from `Shape` and overrides the `area()` function to calculate the area of a circle using the formula `3.14 * radius * radius`.

### Summary of Function overloading and Overriding
Here is a summary list of function overloading and function overriding:
* Rules for function overloading:
    * Functions must have different parameter lists. They cannot have the same number and types of parameters.
    * Functions can have the same name, but different return types. However, this can lead to confusion and should be avoided.
    * Function overloading should be used when different functionality is required based on the input parameters.
    * Avoid overloading operators unless it is necessary or the operator has a well-established meaning.
* Rules for function overriding:
    * The function signature (name, return type, and parameters) must match the base class virtual function.
    * The access specifier must be the same or less restrictive than the base class function.
    * The const qualifier can be added to the overridden function if it was present in the base class function.
    * The override keyword should be used to indicate that the function is intended to override a base class virtual function. This can help catch errors during compilation.
    * Always use virtual functions when defining a function that is intended to be overridden in a derived class.
    * Use virtual destructors in base classes to ensure that the correct destructor is called when deleting objects via pointers to the base class.

To elaborate the last item above, here is an example that illustrates the importance of using a virtual destructor in base classes when deleting objects via pointers to the base class:
```cpp
#include <iostream>

class Base {
public:
    Base() {
        std::cout << "Base constructor" << std::endl;
    }

    virtual ~Base() {
        std::cout << "Base destructor" << std::endl;
    }
};

class Derived : public Base {
public:
    Derived() {
        std::cout << "Derived constructor" << std::endl;
    }

    ~Derived() override {
        std::cout << "Derived destructor" << std::endl;
    }
};

int main() {
    Base* basePtr = new Derived();  // Creating a Derived object through a Base pointer

    delete basePtr;  // Deleting the object via the Base pointer

    return 0;
}
```
In this example, we have a base class called `Base` and a derived class called `Derived` that inherits from `Base`. The base class destructor is declared as virtual, indicating that it should be overridden in derived classes. The derived class destructor is also defined and explicitly marked as an override.

In the `main` function, we create a `Derived` object dynamically using a `Base` pointer. This scenario represents polymorphic behavior, where a base class pointer is used to refer to a derived class object. When we delete the object through the `Base` pointer using `delete basePtr`, it invokes the correct destructor sequence.

The output of the above code, as it is, would be:
```
Base constructor
Derived constructor
Derived destructor
Base destructor
```

This output reflects the construction and destruction sequence of the `Base` and `Derived` objects. 

If we remove the `virtual` keyword from the base class destructor and the `override` keyword from the derived class destructor, the output would still be:
```
Base constructor
Derived constructor
Base destructor
```

### Multiple Inheritance and Polymorphism
Multiple inheritance is a feature in C++ that allows a class to inherit from multiple base classes. This can lead to a problem known as the diamond problem, where two base classes of a derived class have a common base class. To resolve this problem, C++ provides the concept of virtual inheritance.

Using virtual inheritance, we can ensure that the common base class is inherited only once, rather than multiple times. This is achieved by using the `virtual` keyword when declaring the inheritance of a common base class.

Here's an example:
```cpp
class A {
public:
    int x;
};

class B : virtual public A {
public:
    int y;
};

class C : virtual public A {
public:
    int z;
};

class D : public B, public C {
public:
    int sum() {
        return x + y + z;
    }
};
```
In the example above, classes `B` and `C` both inherit from class `A` virtually. This ensures that the variable `x` is inherited only once by class `D`, which inherits from both `B` and `C`.

### Dynamic casting and runtime type information (RTTI)
Dynamic casting and RTTI are other features of C++ that are used in polymorphism. Dynamic casting is a way to check the type of an object at runtime and convert it to a different type. This is useful when working with base class pointers that point to objects of derived classes.

Here's an example:
```cpp
#include <iostream>

using namespace std;

class Base {
public:
    virtual void print() {
        cout << "This is a Base object." << endl;
    }
};

class Derived : public Base {
public:
    void print() override {
        cout << "This is a Derived object." << endl;
    }
};

int main() {
    Base* b = new Derived;
    Derived* d = dynamic_cast<Derived*>(b);
    if (d != nullptr) {
        d->print();
    }
    else {
        cout << "Conversion from Base to Derived failed." << endl;
    }
    delete b;
    return 0;
}
```
In the example above, we create a base class `Base` and a derived class `Derived`. We then create a base class pointer `b` that points to a `Derived` object. We use `dynamic_cast` to cast `b` to a `Derived` pointer `d`. If the conversion from `Base` to `Derived` is successful, the cast will return a non-null pointer, and we can proceed with calling the `print` function of `d`. However, if the conversion fails, the dynamic cast will return a null pointer, indicating that the cast was not successful. We've also included an `else` statement to illustrate the scenario when the conversion fails and added a print statement to inform the user that the conversion from `Base` to `Derived` was unsuccessful.

In C++, `nullptr` is a keyword that represents a null pointer. It is used to initialize or assign a pointer variable when there is no valid memory address to point to. It provides a clear and unambiguous way to indicate the absence of an object or memory location.

Dynamic casting is a type of casting operator in C++ that allows for runtime type checking and conversion of pointers or references to different types within an inheritance hierarchy. It is used when working with polymorphic objects to safely and dynamically determine if a type can be converted to another type.

When used together, `nullptr` and dynamic casting can be useful in scenarios where we want to check if a pointer is valid or if a conversion between related types is possible. For example, dynamic casting can return a null pointer (`nullptr`) if the conversion is not possible, allowing us to handle such cases gracefully and avoid potential runtime errors.

RTTI is a feature of C++ that provides information about the type of an object at runtime. This information can be obtained using the `typeid` operator.

Here's an example:
```cpp
#include <iostream>

using namespace std;

class Animal {
public:
    virtual void speak() {
        cout << "This is an Animal object." << endl;
    }
};

class Dog : public Animal {
public:
    void speak() override {
        cout << "This is a Dog object." << endl;
    }
};

int main() {
    Animal* a = new Dog;
    if (typeid(*a) == typeid(Dog)) {
        cout << "a is a Dog object." << endl;
    }
    delete a;
    return 0;
}
```
In the example above, we create a base class `Animal` and a derived class `Dog`. We then create a base class pointer `a` that points to a `Dog` object. We use the `typeid` operator to check if the type of `*a` is `Dog`. Since the type is `Dog`, we output the message.