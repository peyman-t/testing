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
In this example, we have defined a function template maximum that takes two parameters of the same data type and returns the maximum value of the two. The typename keyword is used to specify that the template parameter can be any data type.

The main function calls the maximum function twice, once with integer values and once with double values. The template parameter is automatically deduced by the compiler based on the type of the parameters passed to the function.

### Template Parameter Deduction
Template parameter deduction is the process by which the compiler automatically determines the template parameter based on the arguments passed to the function.

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
In this example, we have defined a function template `printSize` that takes an array and prints its size. The second template parameter is an integer that represents the size of the array.

The `main` function calls the `printSize` function twice, once with an integer array and once with a double array. The size of the array is automatically deduced by the compiler based on the size of the array passed to the function.