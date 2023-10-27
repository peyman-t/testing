
## Variadic Templates (C++11 onwards):
Variadic templates are a feature introduced in C++11 that allow for functions and classes to accept a variable number of arguments.

### Definition and Syntax of Variadic Templates
Here's an example of a variadic function template that prints a variable number of arguments to the console:
```cpp
#include <iostream>
using namespace std;

// Variadic function template to print a variable number of arguments
template <typename T>
void print(T arg) {
    cout << arg << endl;
}

template <typename T, typename... Args>
void print(T arg, Args... args) {
    cout << arg << ", ";
    print(args...);
}

int main() {
    print(1, 2.5, "Hello", true);

    return 0;
}
```
In this example, we have defined a variadic function template `print` that accepts a variable number of arguments of any data type. The template function is defined using recursive template arguments, with a base case for a single argument, and a recursive case for multiple arguments.

The `main` function calls the `print` function with four arguments of different data types, and the function prints them to the console.

### Creating and Using Variadic Function Templates
Here's an example of creating and using a variadic function template to compute the sum of a variable number of arguments:
```cpp
#include <iostream>
using namespace std;

// Variadic function template to compute the sum of a variable number of arguments
template <typename T>
T sum(T arg) {
    return arg;
}

template <typename T, typename... Args>
T sum(T arg, Args... args) {
    return arg + sum(args...);
}

int main() {
    const int result = sum(1, 2, 3, 4, 5);
    cout << "Sum of 1 to 5 is: " << result << endl;

    return 0;
}
```
In this example, we have defined a variadic function template `sum` that accepts a variable number of arguments of any data type. The template function is defined using recursive template arguments, with a base case for a single argument, and a recursive case for multiple arguments.

The `main` function calls the `sum` function with five integer arguments, and the function computes their sum.

### Creating and Using Variadic Class Templates
Here's an example of creating and using a variadic class template to store a variable number of arguments as a tuple:
```cpp
#include <iostream>
#include <tuple>
using namespace std;

// Variadic class template to store a variable number of arguments as a tuple
template <typename... Args>
class Tuple {
public:
    tuple<Args...> data;

    Tuple(Args... args) : data(args...) {}

    void print() {
        print_helper<0, Args...>();
    }

private:
    template <size_t N, typename T, typename... Rest>
    void print_helper() {
        cout << get<N>(data) << " ";
        if constexpr (sizeof...(Rest) > 0) {
            print_helper<N + 1, Rest...>();
        }
    }
};

int main() {
    Tuple<int, double, string> t(10, 3.5, "Hello");
    t.print();

    return 0;
}
```
In this example, we have defined a variadic class template `Tuple` that stores a variable number of arguments of any data type as a `std::tuple`. The template class is defined using recursive template arguments, with a constructor that accepts the arguments and stores them in the tuple.

The `print` function is used to print the contents of the tuple to the console.

The `main` function creates an instance of the `Tuple` class with three arguments of different data types, and calls the `print` function to print the contents of the tuple to the console.

### Examples of Variadic Templates in C++ Code
Here are a few more examples of variadic templates:
```cpp
// Variadic class template to concatenate a variable number of strings
template <typename... Args>
class Concat {
public:
    static string join(Args... args) {
        stringstream ss;
        (ss << ... << args);
        return ss.str();
    }
};

int main() {
    const string result = Concat<string, string, string>::join("Hello", " ", "World");
    cout << result << endl;

    return 0;
}
```
In this example, we have defined a variadic class template `Concat` that concatenates a variable number of strings. The template class is defined using recursive template arguments, with a static function `join` that accepts the strings and concatenates them using a `stringstream`.

The `main` function creates an instance of the `Concat` class with three string arguments, and calls the `join` function to concatenate them.