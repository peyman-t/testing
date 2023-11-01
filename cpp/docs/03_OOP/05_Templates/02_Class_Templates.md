
## Class Templates
Class templates are similar to function templates, but they define generic classes instead of functions. Class templates allow you to write generic code that can work with any data type. The template parameter is specified inside angle brackets `< >`.

### Definition and Syntax of Class Templates
Here's the basic syntax for a class template:
```cpp
template <typename T>
class MyClass {
public:
    // Member functions and data members go here
};
```
The `template` keyword is used to indicate that this is a class template. The angle brackets `< >` enclose the template parameter list, which can include one or more template parameters.

Inside the class definition, the template parameter can be used like any other data type. For example, you can declare member functions that take a template parameter as a parameter:
```cpp
template <typename T>
class MyClass {
public:
    void setValue(T value) {
        m_value = value;
    }

    T getValue() {
        return m_value;
    }

private:
    T m_value;
};
```
In this example, we have defined a class template `MyClass` that has a data member of type `T` and two member functions that set/get a template parameter `T`.

### Creating and Using Class Templates
Here's an example of creating and using a class template:
```cpp
#include <iostream>
using namespace std;

// Class template for a pair of values
template <typename T1, typename T2>
class Pair {
public:
    T1 first;
    T2 second;

    Pair(T1 a, T2 b) : first(a), second(b) {}
};

int main() {
    Pair<int, double> p1(10, 2.5);
    cout << "p1: " << p1.first << ", " << p1.second << endl;

    Pair<double, char> p2(4.5, 'a');
    cout << "p2: " << p2.first << ", " << p2.second << endl;

    return 0;
}
```
In this example, we have defined a class template `Pair` that holds two values of different data types. The `typename` keyword is used to specify that the template parameters can be any data type.

The `main` function creates two instances of the `Pair` class, one with integer and double values and the other with double and char values. The template parameters are explicitly specified when creating the objects.

### Defining Member Functions for Class Templates
Member functions of a class template can be defined outside of the class definition, just like function templates. Here's an example:
```cpp
#include <iostream>

template <typename T>
class MyClass {
public:
    void setValue(T value);
    T getValue();
private:
    T m_value;
};

template <typename T>
void MyClass<T>::setValue(T value) {
    m_value = value;
}

template <typename T>
T MyClass<T>::getValue() {
    return m_value;
}

int main() {
    // Creates an instance of MyClass with int as the template parameter
    MyClass<int> myObj;

    // Sets the value of myObj to 42 using the setValue function
    myObj.setValue(42);

    // Retrieves the value from myObj using the getValue function
    int value = myObj.getValue();

    // Prints the value
    std::cout << "Value: " << value << std::endl;

    return 0;
}
```
This is a templated class `MyClass` in C++. The class has a member variable `m_value` of type `T`, and two member functions: `setValue` and `getValue`. 

The `setValue` function takes a parameter `value` of type `T` and assigns it to the member variable `m_value`. It does not return any value.

The `getValue` function returns the value stored in the member variable `m_value` of type `T`.

When defining function members outside the class definition, as done here, a separate template declaration is required to specify that the function is part of the templated class `MyClass<T>`. This is necessary because the function is dependent on the template parameter `T`. The template declaration is written as `template <typename T>`, followed by the function definition using the fully-qualified name `MyClass<T>::functionName`.

Therefore, to define function members outside the class definition, the template parameter `T` must be included in both the template declaration and the function definition, as shown in the code.

It's important to stress that the templated class name is `MyClass<T>`, where `T` represents the template parameter. This allows the class to be instantiated with different types when used in code. For example, `MyClass<int>` creates an instance of `MyClass` with `T` as `int`, and `MyClass<double>` creates an instance with `T` as `double`.

In the main function, we create an instance of `MyClass` with `int` as the template parameter using `MyClass<int> myObj;`. We then set the value of `myObj` to 42 using the `setValue` function with `myObj.setValue(42);`. Next, we retrieve the value from `myObj` using the `getValue` function and store it in the `value` variable. Finally, we print the value to the console using `std::cout`.