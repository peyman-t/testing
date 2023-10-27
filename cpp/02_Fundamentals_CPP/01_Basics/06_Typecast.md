
## Type Casting
In C++, type casting is the process of converting a value of one data type to another data type. Type casting is a powerful feature of C++ that allows you to use one data type in place of another data type. This feature is useful when you need to perform arithmetic operations or comparisons between values of different data types. In this lecture, we will discuss the different types of type casting in C++.

### Implicit Type Conversion
Implicit type conversion, also known as implicit type casting, occurs automatically when the compiler converts one data type to another data type without the need for an explicit type cast operator. This occurs when the compiler determines that a value of one data type can be safely converted to a value of another data type. For example:
```cpp
int num1 = 10;
double num2 = num1 / 3.0;
```
In this example, the integer value `10` is implicitly converted to a double value `10.0` before being divided by `3.0`. This is because the division operator requires both operands to be of the same data type.

### Explicit Type Conversion
Explicit type conversion, also known as explicit type casting, occurs when the programmer explicitly specifies a type cast operator to convert a value of one data type to another data type. There are three types of explicit type casting in C++:

#### C-style Type Casting
C-style type casting is a traditional form of type casting that is used in C and C++ programs. C-style type casting uses the following syntax:
```cpp
(new_type) expression
```
In the following example, we use C-style type casting to convert the integer value `10` to a double value before dividing it by `3.0`.
```cpp
#include <iostream>

int main() {
    int intValue = 10;
    double result = (double) intValue / 3.0;

    std::cout << "Result: " << result << std::endl;

    return 0;
}
```

In this example, we have an `int` variable `intValue` with a value of `10`. To ensure that the division is performed as a floating-point division, we use C-style type casting `(double)` to convert `intValue` to a `double` before dividing it by `3.0`. The result of the division is stored in the `result` variable, which will hold the value `3.33333` (approximately).

#### `static_cast`
`static_cast` is a type of casting operator that is used to perform safe and efficient type conversions between different types of data. The syntax of `static_cast` is as follows:
```cpp
static_cast<new_type>(expression)
```
where `new_type` is the type of data to which we want to convert `expression`. `expression` is the value or expression that we want to cast to the new type.

Here is an example of how to use `static_cast` in C++:
```cpp
#include <iostream>

int main() {
    int num1 = 10;
    double num2 = static_cast<double>(num1) / 3;

    std::cout << "num2 = " << num2 << std::endl;

    return 0;
}
```
In this example, we declare two variables, `num1` and `num2`. We initialize `num1` to the integer value 10. We then use `static_cast` to convert `num1` to a double type and divide it by 3. The resulting value is assigned to `num2`.

When we run this program, the output will be:
```cpp
num2 = 3.33333
```
Note that if we don't use `static_cast` in the above program, for example, `double num2 = num1 / 3;` is used, the output will be:
```cpp
num2 = 3
```
since an integer will be divided by 3, and then, the result is put in a double variable.

