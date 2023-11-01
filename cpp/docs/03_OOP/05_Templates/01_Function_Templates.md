## Function Templates
Function templates are similar to class templates, but they define generic functions instead of classes. Function templates allow you to write generic code that can work with any data type. The template parameter is specified inside angle brackets < >.

### Definition and Syntax of Function Templates
Here's the basic syntax for a function template:
```cpp
template <typename T>
T myFunction(T arg1, T arg2) {
    // Function body goes here
}
```
The `template` keyword is used to indicate that this is a function template. The angle brackets `< >` enclose the template parameter list, which can include one or more template parameters.

Inside the function definition, the template parameter can be used like any other data type. In this example, the function takes two arguments of the same data type and returns the same data type.

### Creating and Using Function Templates
Here's an example of creating and using a function template:
```cpp
#include <iostream>
using namespace std;

// Function template to find the maximum of two values
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    int i1 = 10, i2 = 20;
    cout << "Maximum of " << i1 << " and " << i2 << " is " << maximum(i1, i2) << endl;

    double d1 = 2.5, d2 = 4.5;
    cout << "Maximum of " << d1 << " and " << d2 << " is " << maximum(d1, d2) << endl;

    return 0;
}
```
In this example, we have defined a function template `maximum` that takes two parameters of the same data type and returns the maximum value of the two. The `typename` keyword is used to specify that the template parameter can be any data type.

The `main` function calls the `maximum` function twice, once with integer values and once with double values. The template parameter is automatically deduced by the compiler based on the type of the parameters passed to the function.

### Template Argument Deduction
Template argument deduction is the process by which the compiler automatically determines the template argument based on the arguments passed to the function.

Here's an example:
```cpp
#include <iostream>
using namespace std;

// Function template to print the size of an array
template <typename T, int size>
void printSize(T (&arr)[size]) {
    cout << "Size of array: " << size << endl;
}

int main() {
    int arr1[] = {1, 2, 3, 4, 5};
    double arr2[] = {1.1, 2.2, 3.3};

    printSize(arr1); // Output: Size of array: 5
    printSize(arr2); // Output: Size of array: 3

    return 0;
}
```
In this case, the function template `printSize` is defined with two template parameters: `T` and `size`. `T` is a type parameter that can represent any type, and `size` is a non-type parameter that can represent a value, in this case, an integer.

The function `printSize` takes one argument, which is a reference to an array of type `T` and size `size`. The `(&arr)[size]` syntax is used to pass an array by reference to the function. This is necessary because arrays in C++ will otherwise decay to pointers when passed to a function, losing information about their size.

When `printSize` is called with an array, the compiler automatically deduces the type `T` and the size of the array from the argument. This is why you can call `printSize(arr1)` and `printSize(arr2)` without explicitly specifying the type and size of the arrays. The compiler knows that `arr1` is an array of 5 integers and `arr2` is an array of 3 doubles, and it uses this information to instantiate the appropriate versions of the `printSize` function.

The `printSize` function then prints the size of the array, which is the value of the `size` template parameter. This is why the output of the program is "Size of array: 5" and "Size of array: 3".

So, even though non-template parameters may not have been introduced, they are being used here to capture and utilize compile-time information (the size of the array), which is a powerful feature of C++ templates.

### Template Arguments
Let's take look at a simple example:
```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```
In this example, `T` is a template argument that stands for a data type. When you use the `max` function, you can specify the type `T` with the `<>` notation:

```cpp
int main() {
    cout << max<int>(3, 7); // Output: 7
    cout << max<double>(3.14, 2.78); // Output: 3.14
    cout << max<char>('a', 'z'); // Output: 'z'
    return 0;
}
```

In each of these calls to `max`, the type `T` is replaced with the type you specified in `<>`. So `max<int>(3, 7)` uses the `max` function for `int` values, `max<double>(3.14, 2.78)` uses it for `double` values, and so on.

It's worth noting that in many cases, you don't actually need to specify the type in `<>` when you call a function template. The compiler can deduce the type from the arguments you pass to the function. For example, you can write `max(3, 7)` instead of `max<int>(3, 7)`, and the compiler knows that you want to use the `int` version of `max`. As you already saw, this is called template argument deduction.

However, there are cases where you do need to specify the type in `<>`. For example, if you want to call a function template with a specific type that the compiler can't deduce, or if you want to control the type conversion. For example, if you call `max(3, 7.2)`, the compiler doesn't know whether to use `max<int>` or `max<double>`, so you need to specify the type yourself.

### Function Template Instantiation
Function template instantiation in C++ is the process by which the compiler generates a specific version of a function template based on the types of arguments used in a function call. 

When you define a function template, you're essentially defining a whole family of functions, one for each possible type that could be used as a template argument. However, the compiler doesn't actually generate all these functions upfront. Instead, it waits until you call the function template with a specific type, and then it generates (or "instantiates") the specific version of the function you need.

Here's an example of a function template:

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```

This `max` function template can be used with any type `T` that supports the `>` operator. But until you actually call `max` with a specific type, the compiler doesn't generate any code for `max`.

Now, let's say you call `max` with two integers:

```cpp
int main() {
    std::cout << max(3, 7); // Output: 7
    return 0;
}
```

At this point, the compiler sees that you're calling `max` with two integers. So it generates an instance of the `max` function template for the `int` type, replacing `T` with `int` everywhere in the function definition. This is function template instantiation.

The instantiated function looks like this:

```cpp
int max(int a, int b) {
    return (a > b) ? a : b;
}
```

This `int` version of `max` is the function that actually gets called when you do `max(3, 7)`. If later in your code you call `max` with two `double` values, the compiler will instantiate a `double` version of `max`, and so on for any other types you use.

### Abbreviated Function Templates
Abbreviated function templates, also known as "auto" function templates, are a feature introduced in C++20. They allow you to define function templates where the template argument is deduced from the function arguments, without having to explicitly declare a template parameter list.

Here's an example of an abbreviated function template:

```cpp
auto max(auto a, auto b) {
    return (a > b) ? a : b;
}
```

In this example, `auto` is used in place of the template parameter `T` in the function declaration. The compiler will deduce the type of `a` and `b` from the arguments passed to `max`.

You can call this function with arguments of any type that supports the `>` operator, just like with the traditional function template:

```cpp
int main() {
    std::cout << max(3, 7); // Output: 7
    std::cout << max(3.14, 2.78); // Output: 3.14
    std::cout << max('a', 'z'); // Output: 'z'
    return 0;
}
```

Each call to `max` will instantiate a version of the function template for the types of the arguments.