
## Template Type Aliases (C++11 onwards) and typedefs
Template type aliases and typedefs are features introduced in C++11 that allow for defining aliases for complex types and templates.

### Definition and Syntax of Template Type Aliases and typedefs
Here's an example of using a template type alias to define a complex type:
```cpp
#include <vector>
using namespace std;

// Template type alias to define a vector of integers
template <typename T>
using IntVector = vector<T>;

int main() {
    IntVector<int> v = {1, 2, 3, 4, 5};
    for (const auto& i : v) {
        cout << i << " ";
    }
    cout << endl;

    return 0;
}
```
In this example, we have defined a template type alias `IntVector` that defines a vector of a specified data type. The template type alias is defined using the `using` keyword, and is followed by the template parameter and the underlying type.

The `main` function creates a vector of integers using the `IntVector` template type alias, and initializes it with five integer values. The values are then printed to the console.

Here's an example of using a typedef to define a complex type:
```cpp
#include <vector>
using namespace std;

// Typedef to define a vector of integers
typedef vector<int> IntVector;

int main() {
    IntVector v = {1, 2, 3, 4, 5};
    for (const auto& i : v) {
        cout << i << " ";
    }
    cout << endl;

    return 0;
}
```
In this example, we have defined a typedef `IntVector` that defines a vector of integers. The typedef is defined using the `typedef` keyword, and is followed by the underlying type and the alias name.

The `main` function creates a vector of integers using the `IntVector` typedef, and initializes it with five integer values. The values are then printed to the console.

### Creating and Using Template Type Aliases and typedefs
Here's an example of creating and using a template type alias to define a custom container:
```cpp
#include <iostream>
#include <list>
using namespace std;

// Template type alias to define a custom container
template <typename T>
using MyContainer = list<T>;

int main() {
    MyContainer<int> c = {1, 2, 3, 4, 5};
    for (const auto& i : c) {
        cout << i << " ";
    }
    cout << endl;

    return 0;
}
```
In this example, we have defined a template type alias `MyContainer` that defines a custom container using the `std::list` container. The template type alias is defined using the `using` keyword, and is followed by the template parameter and the underlying type.

The `main` function creates a custom container of integers using the `MyContainer` template type alias, and initializes it with five integer values. The values are then printed to the console.

### Examples of Template Type Aliases and typedefs in C++ Code
Here are a few more examples of template type aliases and typedefs:
```cpp
// Template type alias to define a function pointer
template <typename T>
using FunctionPtr = T (*)(int);

// Typedef to define a pointer to a member function
typedef void (MyClass::*MemberFuncPtr)(int);

int main() {
    // Using template type alias to define a function pointer
    FunctionPtr<double> func_ptr = [](int x) -> double
    {
        return x * 2.5;
    };
    const double result = func_ptr(10);
    cout << "Result is: " << result << endl;

    // Using typedef to define a pointer to a member function
    MyClass obj;
    MemberFuncPtr member_func_ptr = &MyClass::member_function;
    (obj.*member_func_ptr)(20);

    return 0;
}
```
In this example, we have defined a template type alias `FunctionPtr` that defines a function pointer with a specified return type and parameter list. The template type alias is defined using the `using` keyword, and is followed by the template parameter and the underlying type.

We have also defined a typedef `MemberFuncPtr` that defines a pointer to a member function of a class. The typedef is defined using the `typedef` keyword, and is followed by the type of the member function and the alias name.

The `main` function uses the template type alias to define a function pointer that multiplies an integer by a double value, and calls the function with an integer argument. It also uses the typedef to define a pointer to a member function of the `MyClass` class, and calls the member function on an instance of the class.