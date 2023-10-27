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
    // Create a shared_ptr to an int
    std::shared_ptr<int> ptr(new int(42));

    // Use the pointer
    std::cout << *ptr << std::endl;

    // The memory is automatically deallocated when the last shared_ptr pointing to the int goes out of scope
    return 0;
}
```
In this example, we create a `std::shared_ptr` pointing to an int with a value of 42. We then use the pointer to print the value of the int. When the last `std::shared_ptr` pointing to the int goes out of scope, the memory allocated to the int is automatically deallocated.

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
    // Create a shared_ptr with a custom deleter
    std::shared_ptr<int> ptr(new int(42), &custom_deleter);

    // Use the pointer
    std::cout << *ptr << std::endl;

    // The custom deleter is called when the last shared_ptr pointing to the int goes out of scope
    return 0;
}
```
In this example, we create a `std::shared_ptr` pointing to an int with a value of 42, and we specify a custom deleter function called `custom_deleter`. When the last `std::shared_ptr` pointing to the int goes out of scope, the `custom_deleter` function is called to deallocate the memory.

### Using `std::make_shared` to Create `std::shared_ptr` Instances
`std::make_shared` is a utility function that can be used to create `std::shared_ptr` instances more efficiently than using the new operator. This is because `std::make_shared` combines memory allocation and object construction into a single step, which can lead to better performance and exception safety. Here's an example:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Create a shared_ptr to an int using make_shared
    std::shared_ptr<int> ptr = std::make_shared<int>(42);

    // Use the pointer
    std::cout << *ptr << std::endl;

    // The memory is automatically deallocated when the last shared_ptr pointing to the int goes out of scope
    return 0;
}
```
In this example, we create a `std::shared_ptr` pointing to an int with a value of 42 using `std::make_shared`. We then use the pointer to print the value of the int. When the last `std::shared_ptr` pointing to the int goes out of scope, the memory allocated to the int is automatically deallocated.

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
In this example, we create a `std::shared_ptr` pointing to a `MyClass` object with a value of 42. We then use the pointer to call the doSomething method of the `MyClass` object. When the last `std::shared_ptr` pointing to the `MyClass` object goes out of scope at the end of the `main` function, the memory allocated to the `MyClass` object is automatically deallocated.
