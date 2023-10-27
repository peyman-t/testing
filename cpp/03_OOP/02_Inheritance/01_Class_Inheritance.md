## Introduction to Inheritance
In C++, inheritance is a mechanism that allows a class to derive properties (data and methods) from another class. The derived class is known as the child or subclass, while the base class is known as the parent or superclass. Inheritance provides several benefits, such as code reuse, modularity, and extensibility.

### Definition of Inheritance
Inheritance is a way to create a new class from an existing class. The new class can inherit the properties of the existing class, such as data members and member functions.

### Benefits of Using Inheritance
The main benefits of using inheritance are:

* Code reuse: Instead of writing the same code multiple times, we can reuse the code from the base class in the derived class.
* Modularity: Inheritance allows us to break down a complex system into simpler, more manageable parts.
* Extensibility: Inheritance allows us to add new functionality to an existing class without modifying its implementation.

## Base (parent) and Derived (child) Classes
Inheritance involves two classes, the base class and the derived class. The base class is also known as the parent class or superclass, while the derived class is also known as the child class or subclass. The derived class inherits properties from the base class and can add its own properties as well.

In C++, inheritance is denoted using the colon (`:`) symbol followed by the access specifier (public, protected or private) and the name of the base class. The general syntax for declaring a derived class is as follows:
```cpp
class DerivedClass : access_specifier BaseClass {
    // member variables and member functions
};
```
Here, `DerivedClass` is the derived class that inherits from the `BaseClass`. `access_specifier` determines the visibility of the inherited members in the derived class. The three possible access specifiers are: 
* `public`: The public members of the base class are accessible in the derived class with the same access level.
* `protected`: The public and protected members of the base class are accessible in the derived class as protected members.
* `private`: The public and protected members of the base class are accessible in the derived class as private members.

Example:
```cpp
class Vehicle {
public:
    int numWheels;
    int maxSpeed;

    void drive() {
        std::cout << "Driving at " << maxSpeed << "mph" << std::endl;
    }
};

class Car : public Vehicle {
public:
    int numDoors;

    void honk() {
        std::cout << "Honking horn" << std::endl;
    }
};

int main() {
    Car c;
    c.numWheels = 4;
    c.maxSpeed = 100;
    c.numDoors = 2;

    c.drive(); // Output: "Driving at 100mph"
    c.honk(); // Output: "Honking horn"

    return 0;
}
```
In this example, the `Vehicle` class is the base class, and the `Car` class is the derived class. The `Car` class inherits the `numWheels` and `maxSpeed` properties from the `Vehicle` class and adds its own property, `numDoors`. The `Car` class also defines its own method, `honk()`. The `Car` object can access both the `Vehicle` class's `drive()` method and the `Car` class's `honk()` method.

## Types of Inheritance
In C++, there are several types of inheritance that can be used to derive a new class from an existing class. They are:

### Single Inheritance
In single inheritance, a derived class is derived from a single base class. It forms a parent-child relationship between the base and derived class.

Example:
```cpp
class Base {
public:
    void foo() {}
};

class Derived : public Base {
public:
    void bar() {}
};
```

### Multiple Inheritance
In multiple inheritance, a derived class is derived from multiple base classes. It forms a diamond-shaped relationship between the derived and base classes.

Example:
```cpp
class Base1 {
public:
    void foo() {}
};

class Base2 {
public:
    void bar() {}
};

class Derived : public Base1, public Base2 {
public:
    void baz() {}
};
```

### Multilevel Inheritance
In multilevel inheritance, a derived class is derived from a base class, which is also derived from another base class. It forms a parent-child-grandchild relationship between the classes.

Example:
```cpp
class Grandparent {
public:
    void foo() {}
};

class Parent : public Grandparent {
public:
    void bar() {}
};

class Child : public Parent {
public:
    void baz() {}
};
```

### Hierarchical Inheritance
In hierarchical inheritance, multiple derived classes are derived from a single base class. It forms a parent-multiple children relationship between the classes.

Example:
```cpp
class Base {
public:
    void foo() {}
};

class Derived1 : public Base {
public:
    void bar() {}
};

class Derived2 : public Base {
public:
    void baz() {}
};
```

### Hybrid Inheritance
Hybrid inheritance is a combination of multiple inheritance and hierarchical inheritance. It forms a complex relationship between the classes.

Example:
```cpp
class Base1 {
public:
    void foo() {}
};

class Base2 {
public:
    void bar() {}
};

class Derived1 : public Base1 {
public:
    void baz() {}
};

class Derived2 : public Base1, public Base2 {
public:
    void qux() {}
};
```

## Constructors and Destructors in Inheritance
Constructors and destructors are special member functions in C++ that are used to initialize and destroy objects of a class, respectively. When a derived class is created, it has its own set of member variables and functions, as well as those inherited from its base class(es). Therefore, constructors and destructors in derived classes have some additional considerations to take into account.

### Syntax for Derived Class Constructors
The syntax for a derived class constructor is as follows:
```cpp
DerivedClassName::DerivedClassName(derived-class-arguments, base-class-arguments)
    : BaseClassName(base-class-arguments)
{
    // Derived class constructor code
}
```
The derived class constructor calls the constructor of its base class(es) by passing the required arguments, which are specified in the initializer list using the syntax `BaseClassName(base-class-arguments)`. This ensures that the base class(es) are properly initialized before the derived class constructor is executed.

Example:
```cpp
#include <iostream>

class Animal {
public:
    Animal(int age) : m_age(age) {
        std::cout << "Animal constructor called" << std::endl;
    }
    virtual ~Animal() {
        std::cout << "Animal destructor called" << std::endl;
    }
protected:
    int m_age;
};

class Cat : public Animal {
public:
    Cat(int age, const std::string& name) : Animal(age), m_name(name) {
        std::cout << "Cat constructor called" << std::endl;
    }
    ~Cat() override {
        std::cout << "Cat destructor called" << std::endl;
    }
private:
    std::string m_name;
};

int main() {
    Cat cat(3, "Whiskers");
    return 0;
}
```
In this example, we have an `Animal` base class and a `Cat` derived class. The `Cat` constructor takes two arguments: an `age` and a `name`. The `Cat` constructor first calls the `Animal` constructor using the syntax `Animal(age)` in the initializer list. Then, it initializes its own `m_name` member variable using the `name` argument.

When we create a `Cat` object in main, we pass the values `3` and `"Whiskers"` as arguments to the `Cat` constructor. The `Cat` constructor first calls the `Animal` constructor with the argument `3`, and then initializes its own `m_name` member variable with the value `"Whiskers"`. Finally, the `Cat` constructor outputs a message indicating that it has been called.

When the main function ends, the `Cat` object is destroyed. First, the `Cat` destructor is called, which outputs a message indicating that it has been called. Then, the `Animal` destructor is called, which also outputs a message indicating that it has been called. The order of destruction is the reverse of the order of construction, which is why the `Cat` destructor is called before the `Animal` destructor.

### Syntax for Derived Class Destructors
The syntax for a derived class destructor is as follows:
```cpp
DerivedClassName::~DerivedClassName()
{
    // Derived class destructor code
}
```
The derived class destructor does not need to explicitly call the destructor of its base class(es), as this is automatically done by the compiler.

## Access Control and Inheritance
In C++, access specifiers (public, protected, and private) control the visibility of class members (i.e., data members and member functions) to the outside world. When a class is inherited, the access specifiers of the base class determine how the derived class can access the base class members.

* **Public inheritance**: In public inheritance, public members of the base class become public members of the derived class, protected members of the base class become protected members of the derived class, and private members of the base class are not accessible in the derived class.
* **Protected inheritance**: In protected inheritance, public and protected members of the base class become protected members of the derived class, and private members of the base class are not accessible in the derived class.
* **Private inheritance**: In private inheritance, public and protected members of the base class become private members of the derived class, and private members of the base class are not accessible in the derived class.

Access specifiers in the derived class can further restrict the visibility of the inherited base class members. For example, a public member of the base class may become protected or private in the derived class. However, it is not possible to increase the visibility of a base class member in the derived class.

Example:
```cpp
class Animal {
public:
    void eat() { std::cout << "Animal is eating" << std::endl; }
protected:
    void sleep() { std::cout << "Animal is sleeping" << std::endl; }
private:
    void move() { std::cout << "Animal is moving" << std::endl; }
};

class Cat : public Animal {
public:
    void play() {
        eat();     // OK: public member of base class
        sleep();   // OK: protected member of base class
        // move(); // Error: private member of base class
    }
};

class Lion : protected Animal {
public:
    void hunt() {
        eat();     // OK: public member of base class
        sleep();   // OK: protected member of base class
        // move(); // Error: private member of base class
    }
};

class Tiger : private Animal {
public:
    void jump() {
        eat();     // OK: public member of base class
        sleep();   // OK: protected member of base class
        // move(); // Error: private member of base class
    }
};
```

In the case of the `Cat` class, it has public inheritance from `Animal`, which means that all public members of `Animal` are accessible by `Cat` objects. Protected members of `Animal` become protected members of `Cat`, and private members of `Animal` are not accessible by `Cat` objects.

In the case of the `Lion` class, it has protected inheritance from `Animal`, which means that all public and protected members of `Animal` become protected members of `Lion`. Private members of `Animal` are not accessible by `Lion` objects.

In the case of the `Tiger` class, it has private inheritance from `Animal`, which means that all public and protected members of `Animal` become private members of `Tiger`. Private members of `Animal` are not accessible by `Tiger` objects.

Here are three separate classes that extend public from `Cat`, `Lion`, and `Tiger` classes, respectively, and show that private and protected members of `Animal` cannot be accessed:
```cpp
class HouseCat : public Cat {
public:
    void groom() {
        eat();     // OK: public member of base class
        sleep();   // OK: protected member of base class
        // move(); // Error: private member of base class
    }
};

class AsiaticLion : public Lion {
public:
    void roar() {
        eat();     // OK: since it became protected member of base class
        sleep();   // OK: protected member of base class
        // move(); // Error: private member of base class
    }
};

class BengalTiger : public Tiger {
public:
    void swim() {
        // eat();    // Error: since it became private member of Tiger class
        // sleep();  // Error: since it became private member of Tiger class
        // move();   // Error: private member of base class
    }
};
```
The accessibility of the members in the derived classes `HouseCat`, `AsiaticLion`, and `BengalTiger` is determined by the accessibility of the corresponding members in their base classes `Cat`, `Lion`, and `Tiger`. In this case, the base classes are already derived from `Animal`, which has public, protected, and private members. As a result, when the derived classes inherit from `Cat`, `Lion`, and `Tiger`, they inherit the access specifiers of the members of their respective base classes. So, the derived classes can access the public and protected members of their base classes, but they cannot access the private members. This is why in `BengalTiger`, the `eat()` and `sleep()` functions cannot be called since they have become private in `Tiger`.
