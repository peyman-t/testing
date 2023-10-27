## `std::unique_ptr` (C++11 onwards)
### Overview of `std::unique_ptr`
`std::unique_ptr` is a type of smart pointer in C++ that represents unique ownership of a dynamically allocated object. This means that there can only be one `std::unique_ptr` pointing to a particular object, and when that `std::unique_ptr` goes out of scope or is explicitly deleted, the memory allocated to that object is automatically deallocated. This helps to avoid memory leaks and dangling pointers.

### Use Cases and Benefits of Using `std::unique_ptr`
Some use cases and benefits of using `std::unique_ptr` include:
* **Single ownership**: `std::unique_ptr` enforces single ownership semantics, which means that there can only be one owner of a particular resource. This helps to avoid bugs caused by multiple objects attempting to deallocate the same memory.
* **Automatic deletion**: `std::unique_ptr` automatically deallocates memory when it goes out of scope or is explicitly deleted. This helps to avoid memory leaks and dangling pointers.
* **Resource management**: `std::unique_ptr` is useful for managing resources such as files, network connections, and locks. When the `std::unique_ptr` goes out of scope or is explicitly deleted, the resource is automatically released.

### Syntax and Usage of `std::unique_ptr`
Here's an example of how to create and use a `std::unique_ptr` in C++:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Create a unique_ptr to an int
    std::unique_ptr<int> ptr(new int(42));

    // Use the pointer
    std::cout << *ptr << std::endl;

    // The memory is automatically deallocated when ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an int with a value of 42. We then use the pointer to print the value of the int. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the memory allocated to the int is automatically deallocated.

### Custom Deleters with `std::unique_ptr`
`std::unique_ptr` also supports custom deleters, which allow you to specify a function or object that will be called to deallocate the memory instead of the default delete operator. This is useful for managing resources that require a different deallocation function than delete. Here's an example:
```cpp
#include <memory>
#include <iostream>

void custom_deleter(int *p) {
    std::cout << "Custom deleter called" << std::endl;
    delete p;
}

int main() {
    // Create a unique_ptr with a custom deleter
    std::unique_ptr<int, decltype(&custom_deleter)> ptr(new int(42), &custom_deleter);

    // Use the pointer
    std::cout << *ptr << std::endl;

    // The custom deleter is called when ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an int with a value of 42, and we specify a custom deleter function called `custom_deleter`. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the `custom_deleter` function is called to deallocate the memory.

### Moving and Transferring Ownership of `std::unique_ptr` Objects
`std::unique_ptr` objects can be moved and their ownership can be transferred to another `std::unique_ptr` object using the `std::move` function. Here's an example:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Create a unique_ptr to an int
    std::unique_ptr<int> ptr(new int(42));

    // Move the pointer to another unique_ptr
    std::unique_ptr<int> ptr2 = std::move(ptr);

    // ptr is now null, and ptr2 owns the memory
    std::cout << (ptr == nullptr) << std::endl;
    std::cout << *ptr2 << std::endl;

    // The memory is automatically deallocated when ptr2 goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an `int` with a value of 42. We then move the pointer to another `std::unique_ptr` object called `ptr2` using the `std::move` function. After the move, `ptr` is null and `ptr2` owns the memory. When `ptr2` goes out of scope at the end of the `main` function, the memory allocated to the `int` is automatically deallocated.

### Examples of Using `std::unique_ptr` in C++ Code
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

    // The memory is automatically deallocated when ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to a `MyClass` object with a value of 42. We then use the pointer to call the `doSomething` method of the `MyClass` object. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the memory allocated to the `MyClass` object is automatically deallocated.
