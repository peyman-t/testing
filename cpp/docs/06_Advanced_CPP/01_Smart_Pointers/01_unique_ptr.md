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
    // Creates a unique_ptr to an int
    std::unique_ptr<int> ptr(new int(42));

    // Uses the pointer
    std::cout << *ptr << std::endl;

    // The memory is automatically deallocated when ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an `int` with a value of 42. We then use the pointer to print the value of the `int`. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the memory allocated to the `int` is automatically deallocated.

### Custom Deleters with `std::unique_ptr`
`std::unique_ptr` also supports custom deleters, which allow you to specify a function or object that will be called to deallocate the memory instead of the default `delete` operator. This is useful for managing resources that require a different deallocation function than `delete`. 

It's worth noting that it might not be immediately clear when custom deleters are really needed. For instance, one might consider pointers to objects whose destructors already release the allocated memory. Nonetheless, there are scenarios where custom deleters provide added flexibility.

Here's an example:
```cpp
#include <memory>
#include <iostream>

void custom_deleter(int *p) {
    std::cout << "Custom deleter called" << std::endl;
    delete p;
}

int main() {
    // Creates a unique_ptr with a custom deleter
    std::unique_ptr<int, decltype(&custom_deleter)> ptr(new int(42), &custom_deleter);

    // Uses the pointer
    std::cout << *ptr << std::endl;

    // The custom deleter is called when ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an `int` with a value of 42, and we specify a custom deleter function called `custom_deleter`. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the `custom_deleter` function is called to deallocate the memory.


`decltype` used above in the code is a keyword introduced in C++11 that is used to query the type of an expression. It stands for "declare type." The primary purpose of `decltype` is to deduce the type of an expression without actually evaluating it. This can be particularly useful in template programming and generic code where the type of an expression might be dependent on template parameters or other factors.

Here's a basic overview of how `decltype` works:

1. **Simple Usage**:
   ```cpp
   int x = 10;
   decltype(x) y = 20;  // y is of type int because x is int
   ```

2. **With Expressions**:
   If you use `decltype` with an expression, it deduces the type that the expression would return.
   ```cpp
   double a = 5.5, b = 2.2;
   decltype(a * b) result;  // result is of type double
   ```

3. **Reference Types**:
   `decltype` can also deduce reference types.
   ```cpp
   int x = 10;
   int& ref_x = x;
   decltype(ref_x) y = x;  // y is of type int&
   ```

### Ownership Transfer with `std::unique_ptr`
In C++, `std::unique_ptr` represents a unique ownership model, meaning that at any given time, only one `std::unique_ptr` can own a particular object in memory. When you move a `std::unique_ptr` object using the `std::move` function, you're essentially transferring this unique ownership to another `std::unique_ptr`. After the transfer, the original pointer relinquishes its ownership and becomes null, ensuring that the object's ownership is held by only one unique pointer at a time.

 Here's an example:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Creates a unique_ptr to an int
    std::unique_ptr<int> ptr(new int(42));

    // Moves the pointer to another unique_ptr
    std::unique_ptr<int> ptr2 = std::move(ptr);

    // ptr is now null, and ptr2 owns the memory
    std::cout << ((ptr == nullptr) ? "ptr is null" : "ptr is not null") << std::endl;
    std::cout << *ptr2 << std::endl;

    // The memory is automatically deallocated when ptr2 goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to an `int` with a value of 42. We then move the pointer to another `std::unique_ptr` object called `ptr2` using the `std::move` function. After the move, `ptr` is null and `ptr2` owns the memory. When `ptr2` goes out of scope at the end of the `main` function, the memory allocated to the `int` is automatically deallocated.

It's important to note that ownership cannot be transferred if the `std::unique_ptr` is declared as `const`, as this would violate the immutability guaranteed by the `const` qualifier.

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
        std::cout << "MyClass::doSomething called" << std::endl;
    }

private:
    int value_;
};

int main() {
    // Creates a unique_ptr to a MyClass object
    std::unique_ptr<MyClass> ptr(new MyClass(42));

    // Uses the pointer
    ptr->doSomething();

    // The memory is automatically deallocated when ptr goes out of scope
    return 0;
}
```
In this example, we create a `std::unique_ptr` pointing to a `MyClass` object with a value of 42. We then use the pointer to call the `doSomething` method of the `MyClass` object. When the `std::unique_ptr` goes out of scope at the end of the `main` function, the memory allocated to the `MyClass` object is automatically deallocated.
