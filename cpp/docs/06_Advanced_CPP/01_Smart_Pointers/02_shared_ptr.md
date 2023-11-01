## `std::shared_ptr` (C++11 onwards)
`std::shared_ptr` is a type of smart pointer in C++ that represents shared ownership of a dynamically allocated object. This means that multiple `std::shared_ptr` objects can point to the same object, and the memory allocated to that object is automatically deallocated when the last `std::shared_ptr` pointing to that object goes out of scope or is explicitly deleted.

### Use Cases and Benefits of Using `std::shared_ptr`
Some use cases and benefits of using `std::shared_ptr` include:
* Shared ownership: `std::shared_ptr` allows multiple objects to share ownership of a particular resource. This is useful for managing resources that are used in multiple places throughout the program.
* Reference counting: `std::shared_ptr` uses a reference counting mechanism to keep track of the number of objects pointing to a particular resource. When the reference count reaches zero, the memory allocated to that resource is automatically deallocated.
* Automatic deletion: `std::shared_ptr` automatically deallocates memory when the last std::shared_ptr pointing to a particular resource goes out of scope or is explicitly deleted.

### Syntax and Usage of `std::shared_ptr`
Here's an example of how to create and use a `std::shared_ptr` in C++:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Creates a shared_ptr to an int
    std::shared_ptr<int> ptr1(new int(42));

    {
        // Creates another shared_ptr pointing to the same int
        std::shared_ptr<int> ptr2 = ptr1;

        std::cout << "Inside the inner scope:" << std::endl;
        std::cout << "*ptr1: " << *ptr1 << std::endl;
        std::cout << "*ptr2: " << *ptr2 << std::endl;
    } // ptr2 goes out of scope here, but the memory is not deallocated because ptr1 still points to it

    std::cout << "\nOutside the inner scope:" << std::endl;
    std::cout << "*ptr1: " << *ptr1 << std::endl;

    {
        // Creates yet another shared_ptr pointing to the same int
        std::shared_ptr<int> ptr3 = ptr1;

        std::cout << "\nInside another inner scope:" << std::endl;
        std::cout << "*ptr1: " << *ptr1 << std::endl;
        std::cout << "*ptr3: " << *ptr3 << std::endl;
    } // ptr3 goes out of scope here, but the memory is not deallocated because ptr1 still points to it

    // The memory is automatically deallocated when ptr1 goes out of scope at the end of the main function
    return 0;
}
```
In this code, the inner scopes demonstrate how the memory remains allocated as long as there's at least one `std::shared_ptr` pointing to it. When all shared pointers that point to the same memory go out of scope, the memory is deallocated.

### Custom Deleters with `std::shared_ptr`
`std::shared_ptr` also supports custom deleters, which allow you to specify a function or object that will be called to deallocate the memory instead of the default delete operator. This is useful for managing resources that require a different deallocation function than delete. Here's an example:
```cpp
#include <memory>
#include <iostream>

void custom_deleter(int *p) {
    std::cout << "Custom deleter called" << std::endl;
    delete p;
}

int main() {
    // Creates a shared_ptr with a custom deleter
    std::shared_ptr<int> ptr1(new int(42), &custom_deleter);

    // Creates another shared_ptr pointing to the same int and using the same custom deleter
    std::shared_ptr<int> ptr2 = ptr1;

    // Uses the pointers
    std::cout << "*ptr1: " << *ptr1 << std::endl;
    std::cout << "*ptr2: " << *ptr2 << std::endl;

    {
        // Creates yet another shared_ptr pointing to the same int and using the same custom deleter
        std::shared_ptr<int> ptr3 = ptr1;
        std::cout << "\nInside inner scope:" << std::endl;
        std::cout << "*ptr3: " << *ptr3 << std::endl;
    } // ptr3 goes out of scope here, but the memory is not deallocated because ptr1 and ptr2 still point to it

    // The custom deleter is called when the last shared_ptr (both ptr1 and ptr2) pointing to the int goes out of scope at the end of the main function
    return 0;
}
```

In this code, the custom deleter will be called only once, when the last `std::shared_ptr` (both `ptr1` and `ptr2`) pointing to the `int` goes out of scope at the end of the `main` function.

### Using `std::make_shared` to Create `std::shared_ptr` Instances
`std::make_shared` is a utility function that can be used to create `std::shared_ptr` instances more efficiently than using the new operator. This is because `std::make_shared` combines memory allocation and object construction into a single step, which can lead to better performance and exception safety. Here's an example:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Creates a shared_ptr to an int using make_shared
    std::shared_ptr<int> ptr1 = std::make_shared<int>(42);

    // Creates another shared_ptr pointing to the same int
    std::shared_ptr<int> ptr2 = ptr1;

    // Uses the pointers
    std::cout << "*ptr1: " << *ptr1 << std::endl;
    std::cout << "*ptr2: " << *ptr2 << std::endl;

    {
        // Creates yet another shared_ptr pointing to the same int
        std::shared_ptr<int> ptr3 = ptr1;
        std::cout << "\nInside inner scope:" << std::endl;
        std::cout << "*ptr3: " << *ptr3 << std::endl;
    } // ptr3 goes out of scope here, but the memory is not deallocated because ptr1 and ptr2 still point to it

    // The memory is automatically deallocated when the last shared_ptr (both ptr1 and ptr2) pointing to the int goes out of scope at the end of the main function
    return 0;
}
```
In this code, all the shared pointers (`ptr1`, `ptr2`, and `ptr3`) point to the same `int` object. The memory for the `int` will be deallocated only when all shared pointers pointing to it go out of scope.

### Examples of Using `std::shared_ptr` in C++ Code
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
        std::cout << "MyClass::doSomething called " << std::endl;
    }

private:
    int value_;
};

int main() {
    // Creates a shared_ptr to a MyClass object
    std::shared_ptr<MyClass> ptr1(new MyClass(42));

    // Creates another shared_ptr pointing to the same MyClass object
    std::shared_ptr<MyClass> ptr2 = ptr1;

    // Uses the pointers
    ptr1->doSomething();
    ptr2->doSomething();

    {
        // Creates yet another shared_ptr pointing to the same MyClass object
        std::shared_ptr<MyClass> ptr3 = ptr1;
        std::cout << "\nInside inner scope:" << std::endl;
        ptr3->doSomething();
    } // ptr3 goes out of scope here, but the memory is not deallocated because ptr1 and ptr2 still point to it

    // The memory is automatically deallocated when the last shared_ptr (both ptr1 and ptr2) pointing to the MyClass object goes out of scope at the end of the main function
    return 0;
}
```
In this code, all the shared pointers (`ptr1`, `ptr2`, and `ptr3`) point to the same `MyClass` object. The memory for the `MyClass` object will be deallocated, and its destructor will be called only when all shared pointers pointing to it go out of scope.