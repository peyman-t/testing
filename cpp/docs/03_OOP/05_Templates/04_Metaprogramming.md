## Template Metaprogramming (Advanced Topics in Templates)
> **Note**
>
> Since from this section to the end of templates, advanced topics are covered, it is recommended to follow only if you would like to learn templates at this level. Otherwise, you can simply skip this section to the end of templates.

Template metaprogramming is a powerful technique in C++ that leverages the template system to perform computations and generate code at compile-time. By exploiting the template mechanism, which is evaluated by the compiler during the compilation process, template metaprogramming allows developers to perform complex computations, type transformations, and code generation without incurring any runtime overhead. This approach shifts computations that would traditionally be performed at runtime to the compile-time phase, enabling optimizations, code specialization, and the ability to generate code based on compile-time conditions and parameters. Template metaprogramming opens up new possibilities for writing more efficient, flexible, and generic code in C++.

Template metaprogramming involves using templates to perform calculations and transformations on types and values at compile-time. The resulting code is executed by the compiler, rather than at runtime.

### Template Metaprogramming Techniques
There are several techniques used in template metaprogramming, including recursion, specialization, and SFINAE.

Recursion involves defining a template function or class that calls itself with different template arguments until a base case is reached.

Specialization involves defining a specialized implementation of a template function or class for a particular data type or set of data types.

SFINAE (Substitution Failure Is Not An Error) involves using template parameters to selectively enable or disable a function or class template based on the type of the arguments.


### Compile-Time Computations Using Templates
First, we present a code without using template metaprogramming to compute the factorial of a number:
```cpp
#include <iostream>

using namespace std;

// Function to compute the factorial of a number at runtime
int factorial(int n) {
    if (n == 0)
        return 1;
    else
        return n * factorial(n - 1);
}

int main() {
    const int result = factorial(5);
    cout << "Factorial of 5 is: " << result << endl;

    return 0;
}
```
In this code, the `factorial` function is defined to calculate the factorial of a number at runtime. It uses a recursive approach where the factorial of 0 is defined as 1, and for any other number `n`, it is computed by multiplying `n` with the factorial of `n-1` using recursion.

In the `main` function, the factorial of 5 is calculated by calling the `factorial` function with the value 5. The result is stored in the `result` variable and printed to the console.

While the template metaprogramming example achieves compile-time computation, this above code performs the factorial calculation at runtime using the recursive function approach.

Here's an example of performing a compile-time factorial computation using templates:
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
The `Factorial` struct is defined as a template struct that takes an integer template parameter `N`. It provides a static constant member variable `value` that represents the factorial of `N`. 

The first part of the template struct `Factorial` provides the general case, where the factorial of `N` is calculated by multiplying `N` with the factorial of `N-1`, recursively. This is achieved by accessing the `value` member variable of `Factorial<N - 1>`. 

The second part of the template specialization is for the base case, where `N` is 0. In this case, the factorial is defined as 1.

In the `main` function, the value of the factorial is computed by accessing the `value` member variable of `Factorial<5>`, representing the factorial of 5. The result is stored in the `result` variable and printed to the console using `cout`. 

By utilizing template specialization, the factorial computation is performed at compile-time, providing a constant value that is available during the compilation process rather than runtime.

### Examples of Template Metaprogramming in C++ Code
First, we write a recursive function to calculate the Fibonacci series:
```cpp
#include <iostream>
using namespace std;

// Function to compute the nth Fibonacci number at runtime
int fibonacci(int n) {
    if (n == 0)
        return 0;
    else if (n == 1)
        return 1;
    else
        return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    const int result = fibonacci(10);
    cout << "The 10th Fibonacci number is: " << result << endl;

    return 0;
}
```
In this code, the `fibonacci` function is defined to calculate the nth Fibonacci number at runtime. It uses a recursive approach where the Fibonacci numbers for n=0 and n=1 are defined as 0 and 1 respectively. For any other value of n, it is computed by summing the two previous Fibonacci numbers using recursion.

In the `main` function, the 10th Fibonacci number is calculated by calling the `fibonacci` function with the value 10. The result is stored in the `result` variable and printed to the console.

Here's an example of using recursion in template metaprogramming to calculate the Fibonacci series:
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

Here are a few more examples of template metaprogramming:
```cpp
#include <iostream>

using namespace std;

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
Here's an explanation of each part:

1. Power Calculation:
   - The `Power` struct template calculates the power of a number at compile-time. It uses template specialization to handle the base case where the power is 0 (returns 1) and the general case where the power is greater than 0 (recursively multiplies the number by the power-1).

2. Type Checking:
   - The `IsPointer` struct template checks if a type is a pointer or not. It uses template specialization to handle the case where the type is a pointer (returns true) and the case where the type is not a pointer (returns false).

3. Array Size Calculation:
   - The `ArraySize` function template computes the size of an array at compile-time. It takes a reference to an array and uses template deduction to determine the size of the array by dividing the size of the array by the size of its elements.

In the `main` function:
- The power of 2 raised to 5 is calculated using the `Power` struct template, and the result is printed.
- The `IsPointer` struct template is used to check if `int*` and `int` are pointers or not, and the results are printed.
- An array `arr` is defined, and the `ArraySize` function template is used to compute the size of the array at compile-time, and the result is printed.

`size_t` is a type in C++ that is typically used to represent the size or count of objects. It is an unsigned integral type, specifically chosen to be able to represent the maximum possible size of any object in memory.

The `size_t` type used in the above example is commonly used in scenarios where the size or count of elements is needed, such as when working with arrays, buffers, or memory allocations. It provides a platform-independent way to express sizes and indices without being affected by the specific size of `int` or `long` on different platforms.

Using `size_t` is particularly important in cases where sizes or indices can potentially exceed the range of other integer types, as `size_t` is designed to be large enough to accommodate the largest possible object on the system.

For example, the `sizeof` operator in C++ returns a value of type `size_t`, indicating the size of an object or type in bytes.

It's worth noting that `size_t` is defined in the `<cstddef>` or `<stddef.h>` header file, so including that header is necessary to use `size_t` in your code.

### Substitution Failure Is Not An Error (SFINAE)
SFINAE is a principle in C++ template metaprogramming that says if a compiler fails to specialize a template with a particular set of template arguments, it should simply ignore that specialization and move on to the next one, rather than treating it as a compilation error.

SFINAE is often used in conjunction with `std::enable_if` to conditionally remove functions from overload resolution based on type traits. This allows you to create different function templates that will be called for different types of arguments.

Here's a simple example. Suppose we want to create a function `print` that behaves differently for integral types and floating-point types:

```cpp
#include <iostream>
#include <type_traits>

// Function to be used when T is an integral type
template <typename T>
typename std::enable_if<std::is_integral<T>::value>::type
print(T value) {
    std::cout << value << " is an integral number.\n";
}

// Function to be used when T is a floating-point type
template <typename T>
typename std::enable_if<std::is_floating_point<T>::value>::type
print(T value) {
    std::cout << value << " is a floating-point number.\n";
}

int main() {
    print(5);        // Output: 5 is an integral number.
    print(3.14);     // Output: 3.14 is a floating-point number.
    return 0;
}
```

In this example, `std::enable_if` is used to enable or disable the two versions of the `print` function depending on the type of the argument. If the argument is an integral type, the first version of `print` is enabled and called. If the argument is a floating-point type, the second version of `print` is enabled and called.

This is a powerful technique that allows you to write more generic and reusable code. However, it can also make the code more complex and harder to understand, so it should be used judiciously.