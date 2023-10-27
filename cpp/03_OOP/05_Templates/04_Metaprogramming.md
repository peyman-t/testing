## Template Metaprogramming
Template metaprogramming is a technique used in C++ to perform computations at compile-time using templates.

### Introduction to Template Metaprogramming
Template metaprogramming involves using templates to perform calculations and transformations on types and values at compile-time. The resulting code is executed by the compiler, rather than at runtime.

### Compile-Time Computations Using Templates
Here's an example of performing a compile-time computation using templates:
```cpp
#include <iostream>
using namespace std;

// Template function to compute the factorial of a number at compile-time
template <int N>
struct Factorial {
    static const int value = N * Factorial<N - 1>::value;
};

template <>
struct Factorial<0> {
    static const int value = 1;
};

int main() {
    const int result = Factorial<5>::value;
    cout << "Factorial of 5 is: " << result << endl;

    return 0;
}
```
In this example, we have defined a template function `Factorial` that computes the factorial of a number at compile-time. The template function is defined recursively, with a base case for `Factorial<0>`.

The `main` function computes the factorial of 5 using the `Factorial` template function, and outputs the result.

### Template Metaprogramming Techniques
There are several techniques used in template metaprogramming, including recursion, specialization, and SFINAE.

Recursion involves defining a template function or class that calls itself with different template arguments until a base case is reached.

Specialization involves defining a specialized implementation of a template function or class for a particular data type or set of data types.

SFINAE (Substitution Failure Is Not An Error) involves using template parameters to selectively enable or disable a function or class template based on the type of the arguments.

Here's an example of using recursion in template metaprogramming:
```cpp
#include <iostream>
using namespace std;

// Template function to compute the nth Fibonacci number at compile-time
template <int N>
struct Fibonacci {
    static const int value = Fibonacci<N - 1>::value + Fibonacci<N - 2>::value;
};

template <>
struct Fibonacci<0> {
    static const int value = 0;
};

template <>
struct Fibonacci<1> {
    static const int value = 1;
};

int main() {
    const int result = Fibonacci<10>::value;
    cout << "The 10th Fibonacci number is: " << result << endl;

    return 0;
}
```
In this example, we have defined a template function `Fibonacci` that computes the nth Fibonacci number at compile-time. The template function is defined recursively, with base cases for `Fibonacci<0>` and `Fibonacci<1>`.

The `main` function computes the 10th Fibonacci number using the `Fibonacci` template function, and outputs the result.

### Examples of Template Metaprogramming in C++ Code
Here are a few more examples of template metaprogramming:
```cpp
// Template function to compute the power of a number at compile-time
template <int N, int M>
struct Power {
    static const int value = N * Power<N, M - 1>::value;
};

template <int N>
struct Power<N, 0> {
    static const int value = 1;
};

// Template function to check if a type is a pointer
template <typename T>
struct IsPointer {
    static const bool value = false;
};

template <typename T>
struct IsPointer<T*>
{
    static const bool value = true;
};

// Template function to compute the size of an array at compile-time
template <typename T, size_t N>
constexpr size_t ArraySize(T(&)[N]) {
    return N;
}

int main() {
    const int power = Power<2, 5>::value;
    cout << "2^5 is: " << power << endl;
    cout << "Is int* a pointer? " << IsPointer<int*>::value << endl;
    cout << "Is int a pointer? " << IsPointer<int>::value << endl;

    int arr[] = {1, 2, 3, 4, 5};
    cout << "Size of array is: " << ArraySize(arr) << endl;

    return 0;
}
```
These examples demonstrate different types of template metaprogramming, including compile-time computation of mathematical operations, checking type traits at compile-time, and computing the size of an array at compile-time.