## Memory management and Exception Safety with Smart Pointers
Smart pointers are an important tool for managing dynamically allocated memory in C++. They provide automatic memory management, which means that the memory allocated to dynamically allocated objects is automatically deallocated when the last smart pointer pointing to the object goes out of scope. This can help prevent memory leaks, which occur when memory is allocated but not deallocated.

In addition to automatic memory management, smart pointers can also help with exception safety in C++. In C++, exceptions can be thrown during the execution of a function. If an exception is thrown and not caught, the program will terminate. Smart pointers can help ensure that dynamically allocated memory is deallocated even if an exception is thrown during the execution of a function.

### Resource Acquisition Is Initialization (RAII) Pattern
Smart pointers are based on the Resource Acquisition Is Initialization (RAII) pattern. The RAII pattern is a technique for managing resources in C++ where the acquisition of a resource is done in the constructor of an object, and the release of the resource is done in the destructor of the object. Smart pointers use this pattern to automatically manage dynamically allocated memory.

### Smart Pointers and Custom Resource Management
Smart pointers can be customized to manage resources other than dynamically allocated memory, such as file handles or network connections. This can be done by providing a custom deleter function to the smart pointer. The deleter function is called when the smart pointer goes out of scope and is responsible for releasing the resource.

### Examples of Using Smart Pointers in C++ Code
Here's an example of using `std::unique_ptr` to manage dynamically allocated memory in C++:
```cpp
#include <memory>
#include <iostream>

class MyClass {
public:
    MyClass(int value) : value_(value) {
        std::cout << "MyClass constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor called" << std::endl;
    }

    void doSomething() {
        std::cout << "MyClass::doSomething called with value " << value_ << std::endl;
    }

private:
    int value_;
};

int main() {
    // Create a unique_ptr to a MyClass object
    std::unique_ptr<MyClass> ptr(new MyClass(42));

    // Use the pointer
    ptr->doSomething();

    // The memory is automatically deallocated when the unique_ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to a `MyClass` object with a value of 42. We then use the pointer to call the `doSomething` method of the `MyClass` object. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the memory allocated to the `MyClass` object is automatically deallocated.

Here's an example of using a custom deleter with `std::unique_ptr` to manage a file handle:
```cpp
#include <memory>
#include <iostream>
#include <fstream>

int main() {
    // Create a unique_ptr to a file
    std::unique_ptr<std::ofstream, void (*)(std::ofstream*)> ptr(new std::ofstream("output.txt"), [](std::ofstream* f) {
        f->close();
        std::cout << "File closed" << std::endl;
    });

    // Use the file
    *ptr << "Hello, world!" << std::endl;

    // The file is automatically closed when the unique_ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an `std::ofstream` object that writes to a file named `output.txt`. We provide a custom deleter function that closes the file and prints a message to the console. We use the `*` operator to dereference the pointer and write the string "Hello, world!" to the file. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the file is automatically closed and the memory allocated to the `std::ofstream` object is automatically deallocated.

Here's an example of using `std::shared_ptr` to manage dynamically allocated memory in C++:
```cpp
#include <memory>
#include <iostream>

class MyClass {
public:
    MyClass(int value) : value_(value) {
        std::cout << "MyClass constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor called" << std::endl;
    }

    void doSomething() {
        std::cout << "MyClass::doSomething called with value " << value_ << std::endl;
    }

private:
    int value_;
};

int main() {
    // Create a shared_ptr to a MyClass object
    std::shared_ptr<MyClass> ptr(new MyClass(42));

    // Use the pointer
    ptr->doSomething();

    // The memory is automatically deallocated when the last shared_ptr pointing to the MyClass object goes out of scope
    return 0;
}
```
In this example, we create a `std::shared_ptr` pointing to a `MyClass` object with a value of 42. We then use the pointer to call the `doSomething` method of the `MyClass` object. When the last `std::shared_ptr` pointing to the `MyClass` object goes out of scope at the end of the `main` function, the memory allocated to the `MyClass` object is automatically deallocated.

## Smart Pointers and Container Classes
Smart pointers can be used with STL containers such as `std::vector`, `std::list`, and `std::map`. When using smart pointers with containers, it's important to remember that the container takes ownership of the objects pointed to by the smart pointers.

Here's an example of using `std::unique_ptr` with `std::vector`:
```cpp
#include <memory>
#include <vector>
#include <iostream>

class MyClass {
public:
    MyClass(int value) : value_(value) {
        std::cout << "MyClass constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor called" << std::endl;
    }

    void doSomething() {
        std::cout << "MyClass::doSomething called with value " << value_ << std::endl;
    }

private:
    int value_;
};

int main() {
    // Create a vector of unique_ptrs to MyClass objects
    std::vector<std::unique_ptr<MyClass>> vec;

    // Add elements to the vector
    vec.push_back(std::make_unique<MyClass>(42));
    vec.push_back(std::make_unique<MyClass>(100));

    // Use the elements in the vector
    for (auto& elem : vec) {
        elem->doSomething();
    }

    // The memory is automatically deallocated when the unique_ptrs go out of scope
    return 0;
}
```
In this example, we create a `std::vector` of `std::unique_ptrs` pointing to `MyClass` objects. We use the `push_back` method to add two `MyClass` objects to the vector. We then use a range-based for loop to call the `doSomething` method of each `MyClass` object. When the `std::unique_ptrs` go out of scope at the end of the `main` function, the memory allocated to the `MyClass` objects is automatically deallocated.

### Guidelines for using smart pointers in containers
When using smart pointers with containers, there are some guidelines to keep in mind:
* Use `std::unique_ptr` if the container takes ownership of the objects.
* Use `std::shared_ptr` if multiple objects need to reference the same object.
* Avoid using raw pointers in containers, as they can lead to memory leaks.

It's also important to remember that the container takes ownership of the objects pointed to by the smart pointers. This means that the objects will be automatically deallocated when the container goes out of scope. If you need to remove an object from the container without deallocating it, you can use a `std::shared_ptr` with a custom deleter function that does nothing.

## Smart Pointers and Inheritance
Smart pointers can be used to manage objects in inheritance hierarchies in C++. When using smart pointers with inheritance hierarchies, it's important to remember that the smart pointer must have a type that is compatible with the type of the base class.

Here's an example of using `std::unique_ptr` with an inheritance hierarchy:
```cpp
#include <memory>
#include <iostream>

class Base {
public:
    virtual void doSomething() {
        std::cout << "Base::doSomething called" << std::endl;
    }

    virtual ~Base() {}
};

class Derived : public Base {
public:
    void doSomething() override {
        std::cout << "Derived::doSomething called" << std::endl;
    }
};

int main() {
    // Create a unique_ptr to a Derived object and call its doSomething method
    std::unique_ptr<Base> ptr(new Derived());
    ptr->doSomething();

    // The memory is automatically deallocated when the unique_ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to a `Derived` object. We use the `->` operator to call the `doSomething` method of the `Derived` object. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the memory allocated to the `Derived` object is automatically deallocated.

### Smart Pointers and Polymorphism
Polymorphism is a key feature of inheritance in C++. Smart pointers can be used to manage polymorphic objects in inheritance hierarchies. When using smart pointers with polymorphic objects, it's important to declare the base class destructor as virtual. This ensures that the destructor of the derived class is called when the object is deleted through a pointer to the base class.

Here's an example of using `std::shared_ptr` with a polymorphic object:
```cpp
#include <memory>
#include <iostream>

class Base {
public:
    virtual void doSomething() {
        std::cout << "Base::doSomething called" << std::endl;
    }

    virtual ~Base() {}
};

class Derived : public Base {
public:
    void doSomething() override {
        std::cout << "Derived::doSomething called" << std::endl;
    }
};

int main() {
    // Create a shared_ptr to a polymorphic object and call its doSomething method
    std::shared_ptr<Base> ptr = std::make_shared<Derived>();
    ptr->doSomething();

    // The memory is automatically deallocated when the last shared_ptr pointing to the object goes out of scope
    return 0;
}
```
In this example, we create a `std::shared_ptr` pointing to a polymorphic object of type Derived, which inherits from Base. We use the `->` operator to call the `doSomething` method of the object. When the last `std::shared_ptr` pointing to the object goes out of scope at the end of the `main` function, the memory allocated to the object is automatically deallocated.