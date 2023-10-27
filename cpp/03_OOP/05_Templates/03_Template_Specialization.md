
## Template Specialization
Template specialization is a technique used to provide a specialized implementation of a template for a particular data type or set of data types.

### Definition and Purpose of Template Specialization
Here's the basic syntax for template specialization:
```cpp
template <typename T>
class MyClass {
    // Generic implementation of MyClass goes here
};

template <>
class MyClass<int> {
    // Specialized implementation of MyClass for int goes here
};
```
In this example, we have defined a generic class template `MyClass` with a template parameter `T`. We've also provided a specialized implementation of `MyClass` for the `int` data type.

The purpose of template specialization is to provide a different implementation for a specific data type or set of data types that cannot be implemented using the generic implementation.

### Full Specialization of Function and Class Templates
Here's an example of full specialization of a class template:
```cpp
#include <iostream>
using namespace std;

// Generic class template for a pair of values
template <typename T1, typename T2>
class Pair {
public:
    T1 first;
    T2 second;

    Pair(T1 a, T2 b) : first(a), second(b) {}
};

// Full specialization of Pair class for char* data type
template <>
class Pair<char*, char*> {
public:
    char* first;
    char* second;

    Pair(char* a, char* b) : first(a), second(b) {}
};

int main() {
    Pair<int, double> p1(10, 2.5);
    cout << "p1: " << p1.first << ", " << p1.second << endl;

    Pair<char*, char*> p2("Hello", "World");
    cout << "p2: " << p2.first << ", " << p2.second << endl;

    return 0;
}
```
In this example, we have defined a generic class template `Pair` that holds two values of different data types. We've also provided a full specialization of `Pair` for the `char*` data type, with a different implementation that is specific to the `char*` data type.

The `main` function creates two instances of the `Pair` class, one with integer and double values and the other with char* values. The template parameters are explicitly specified when creating the objects.

### Partial Specialization of Class Templates
Partial specialization is a technique used to provide a specialized implementation of a template for a subset of data types. Here's an example of partial specialization of a class template:
```cpp
#include <iostream>
using namespace std;

// Generic class template for a pair of values
template <typename T1, typename T2>
class Pair {
public:
    T1 first;
    T2 second;

    Pair(T1 a, T2 b) : first(a), second(b) {}
};

// Partial specialization of Pair class for a pair of the same data type
template <typename T>
class Pair<T, T> {
public:
    T first;
    T second;

    Pair(T a, T b) : first(a), second(b) {}
};

int main() {
    Pair<int, double> p1(10, 2.5);
    cout << "p1: " << p1.first << ", " << p1.second << endl;

    Pair<int, int> p2(5, 7);
    cout << "p2: " << p2.first << ", " << p2.second << endl;

    return 0;
}
```
In this example, we have defined a generic class template `Pair` that holds two values of different data types. We've also provided a partial specialization of `Pair` for a pair of the same data type, with a different implementation that is specific to this case.

The `main` function creates two instances of the `Pair` class, one with integer and double values and the other with integer values. The template parameters are explicitly specified when creating the objects.

### Examples of Template Specialization in C++ Code
Here are a few more examples of template specialization:
```cpp
// Full specialization of a function template
template <>
void myFunction<int>(int arg) {
    cout << "Specialized implementation for int: " << arg << endl;
}

// Partial specialization of a function template
template <typename T>
void myFunction<T*>(T* arg) {
    cout << "Specialized implementation for pointer type: " << *arg << endl;
}

// Full specialization of a class template with a static data member
template <typename T>
class MyClass {
public:
    static int counter;
};

template <typename T>
int MyClass<T>::counter = 0;

template <>
int MyClass<char>::counter = 100;

// Partial specialization of a class template with a member function
template <typename T>
class MyClass {
public:
    void myFunction(T arg);
};

template <>
void MyClass<int>::myFunction(int arg) {
    cout << "Specialized implementation for int: " << arg << endl;
}
```
These examples demonstrate different types of template specialization, including full and partial specialization of function and class templates.