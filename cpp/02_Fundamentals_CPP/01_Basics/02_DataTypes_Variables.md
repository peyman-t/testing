
## Data Types and Variables
Variables and data types are fundamental concepts in C++ programming. Variables are used to store data, while data types define the type and size of the data that can be stored in a variable. In this text, we will elaborate on variables, data types, and their usage in C++ with examples. 

In C++, defining a variable involves specifying its data type, followed by the variable name. Optionally, you can also initialize the variable with an initial value. In the following, you will see different data types and how variables of those data types are defined (and initialized).

### Integer Types
Integer types can store integers, that is, values without decimal points. They come in various sizes and can be signed (allowing negative values) or unsigned (allowing only non-negative values). The following integer types are supported in C++:

At the bachelor level, let's explore the concepts of "signed char" and "unsigned char" in C++. 

In C++, the "char" data type represents a single character. It can hold a wide range of characters, including alphabets, digits, symbols, and control characters. By default, the "char" type is considered to be "signed," which means it can represent both positive and negative values.

However, C++ also provides the ability to explicitly define a "char" as either "signed char" or "unsigned char." Let's delve into each type:

#### Signed Char
A "signed char" is a data type that can hold both positive and negative values, just like a regular "char." The range of values a "signed char" can represent is typically from -128 to 127. The negative values are represented using two's complement notation.

Here's an example to illustrate the usage of "signed char":

```cpp
signed char myChar = -50;
```

In this example, the variable "myChar" is declared as a "signed char" and assigned the value of -50. It can store negative values like -1, -50, or 0 as well as positive values within its range.

#### Unsigned Char
On the other hand, an "unsigned char" is a data type that can only hold non-negative values, ranging from 0 to 255. It cannot represent negative values.

Here's an example demonstrating the usage of "unsigned char":

```cpp
unsigned char myChar = 200;
```
In this case, the variable "myChar" is declared as an "unsigned char" and assigned the value of 200. It can store only non-negative values, such as 0, 1, 200, or 255.

#### `short`
A short integer, typically 2 bytes (16 bits) in size. The range for a signed short is -32,768 to 32,767, while the range for an unsigned short is 0 to 65,535. For example:
```cpp
short signed_short = -32768;
unsigned short unsigned_short = 65535;
```

#### `int`
The `int` data type represents a regular integer in C++. Its size, in terms of bytes, can vary depending on the architecture of the execution environment. Typically, an `int` is 4 bytes (32 bits) in size. The range for a 4-byte signed int is -2,147,483,648 to 2,147,483,647, while the range for an unsigned int is 0 to 4,294,967,295. For example:
```cpp
int signed_int = -2147483648;
unsigned int unsigned_int = 4294967295;
```

#### `long`
A long integer, typically 4 bytes (32 bits) in size. The range for a signed long is -2,147,483,648 to 2,147,483,647, while the range for an unsigned long is 0 to 4,294,967,295. For example:
```cpp
long signed_long = -2147483648L;
unsigned long unsigned_long = 4294967295UL;
```

#### `long long`
A long long integer, typically 8 bytes (64 bits) in size. The range for a signed long long is -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807, while the range for an unsigned long long is 0 to 18,446,744,073,709,551,615. For example:
```cpp
long long signed_long_long = -9223372036854775808LL;
unsigned long long unsigned_long_long = 18446744073709551615ULL;
```

#### Fixed-Size Integers
In C++, the integer types are defined in the ISO standard and are listed in order by size. Each integer type provides at least as much storage as the preceding types in the list. However, it is important to note that the size of each integer type is architecture-dependent, meaning it can vary on different systems.

To ensure consistent and precise control over the storage size of integer variables, especially when a specific number of bits must be used, the `cstdint` header provides integer types with specified bit sizes. These types guarantee that they have the exact number of bits regardless of the underlying architecture.

To ensure a specific number of bits are used, regardless of the architecture, you can utilize the integer types defined in `cstdint`. Here are some examples:

- `int8_t`: This is a signed integer type with a size of 1 byte (8 bits). For example:

  ```cpp
  #include <cstdint>

  int8_t count = -5;
  ```

- `uint16_t`: This is an unsigned integer type with a size of 2 bytes (16 bits). For example:

  ```cpp
  #include <cstdint>

  uint16_t quantity = 1000;
  ```

By using the integer types provided by the ISO standard and `cstdint`, you can ensure portability, precise control over storage size, and consistent behavior of your code across different systems and compilers.

#### Usage of Integer Suffixes
In C++, you can use integer suffixes to specify the type of integer literals and control their size and signedness. The commonly used integer suffixes are:

- `L` (or `l`): This suffix is used to indicate a long integer literal. It is typically used when the value exceeds the range of a regular `int` and needs to be stored in a larger integer type, such as `long` or `long long`. For example:

  ```cpp
  long largeNumber = 1000000L;
  ```

- `LL` (or `ll`): This suffix is used to indicate a long long integer literal. It is used when the value requires even more storage than a regular `long` integer. It is commonly used for very large numbers. For example:

  ```cpp
  long long hugeNumber = 123456789012345LL;
  ```

- `UL` (or `ul`): This suffix is used to indicate an unsigned long integer literal. It is typically used when the value is intended to be stored in an unsigned `long` integer. For example:

  ```cpp
  unsigned long positiveValue = 5000UL;
  ```

- `ULL` (or `ull`): This suffix is used to indicate an unsigned long long integer literal. It is used when the value requires more storage than an unsigned `long` integer. It is commonly used for very large unsigned numbers. For example:

  ```cpp
  unsigned long long veryLargeValue = 123456789012345ULL;
  ```

It is important to use the appropriate suffix to ensure that the literal is interpreted correctly by the compiler. Using the correct suffix helps in avoiding potential truncation, narrowing, or sign-related issues. Choosing the appropriate suffix ensures that the literal is assigned to the correct integer type and follows the desired signedness.

### Floating-Point Types
Floating-point types can store real numbers, including decimal values and scientific notation. They come in two sizes: single-precision (float) and double-precision (double).

#### `float`
A single-precision floating-point number, typically 4 bytes (32 bits) in size. It has a range of approximately ±3.4E-38 to ±3.4E+38, with about 7 decimal digits of precision. For example:
```cpp
float single_precision = 3.14159f;
```

#### `double`
A double-precision floating-point number, typically 8 bytes (64 bits) in size. It has a range of approximately ±1.7E-308 to ±1.7E+308, with about 15 decimal digits of precision. For example:
```cpp
double double_precision = 3.141592653589793;
```

#### `long double`
In C++, `long double` is a floating-point data type that represents extended precision floating-point numbers. It provides a larger range and higher precision compared to the regular `double` data type.

The `long double` type is implementation-dependent, meaning its size and precision can vary across different platforms and compilers. On most systems, `long double` is implemented as a 10-byte (80-bit) or 12-byte (96-bit) floating-point representation.

`long double` variables can be declared and initialized like any other data type in C++. For example:

```cpp
  long double pi = 3.141592653589793238462643383279502884L;
```
Note that the `L` suffix is used to indicate a `long double` literal.

Floating-point types can indeed be a source of confusion and bugs in programming, especially due to the limitations of representing certain decimal values precisely. One notable example is the fact that numbers like 0.1 cannot be represented exactly by the float or double data types.

The reason behind this limitation lies in the way floating-point numbers are stored and represented in binary format. Floating-point numbers use a fixed number of bits to represent a wide range of values, including both integer and fractional parts. However, not all decimal numbers can be precisely represented using a finite number of binary digits.

In the case of 0.1, which is a recurring decimal in base-10 representation, it cannot be expressed exactly in binary. When storing 0.1 in a float or double variable, the actual stored value is an approximation. This approximation can lead to small rounding errors or discrepancies when performing calculations involving decimal values.

### Boolean Type
#### `bool`
The `bool` data type in C++ is a built-in primitive type used to represent boolean values, which can only be `true` or `false`. It is primarily used to represent the truth values of logical expressions and control the flow of a program by making decisions based on conditions.

The size of a `bool` data type is typically 1 byte, but it may vary depending on the platform and compiler. In C++, the keywords `true` and `false` are used to represent boolean values, and they are equivalent to the integer values 1 and 0, respectively. Here are some examples of using the bool data type in C++:
```cpp
bool is_happy = true;
bool is_raining = false;
```

### Character Types
These data types are essential for handling text and character-based information in a program. We will discuss the character data types in C++, their sizes, and provide examples to illustrate their usage.

#### `char`
This is the most basic character data type in C++, used for storing single-byte characters (usually 8 bits) represented by the ASCII encoding. The char type can store both positive and negative values, which represent the corresponding ASCII characters. The size of a char is typically 1 byte, but it may vary depending on the platform and compiler.
```cpp
char letter = 'A';
char digit = '7';
char symbol = '#';
```
It's worth noting that the char type can also be used to store small integer values since it's essentially an integer type. However, it's recommended to use char primarily for storing characters.

Here is a part of the ASCII table along with a brief explanation:

```
Character  | ASCII Value | Description
-------------------------------------
   'A'     |     65      | Uppercase letter A
   'B'     |     66      | Uppercase letter B
   'C'     |     67      | Uppercase letter C
   ...     |     ...     | ...
   'Z'     |     90      | Uppercase letter Z
```

The ASCII table is a standardized character encoding scheme that assigns numeric values to characters. Each character is represented by a unique ASCII value. In the example above, we show the uppercase letters 'A' to 'Z' along with their corresponding ASCII values. For instance, the character 'A' is represented by the ASCII value 65. The ASCII table allows computers to store and process text using numerical representations.

#### `wchar_t`
This data type is used for storing wide characters, which are larger than single-byte characters and are typically used for representing Unicode characters or multibyte character sets. The size of wchar_t varies depending on the platform and compiler but is generally 2 or 4 bytes.
```cpp
wchar_t japanese_char = L'あ'; // A Japanese hiragana character
wchar_t greek_char = L'Δ'; // A Greek capital letter delta
```

#### `char16_t` and `char32_t`
These are fixed-size character types introduced in C++11, designed specifically for handling Unicode characters. `char16_t` has a size of 2 bytes (16 bits) and can store Unicode characters in the UTF-16 encoding, while `char32_t` has a size of 4 bytes (32 bits) and can store Unicode characters in the UTF-32 encoding.
```cpp
const char16_t emoji_u16[] = u"\U0001F600"; // A Unicode emoji character in UTF-16
const char32_t emoji_u32 = U'\U0001F600'; // The same Unicode emoji character in UTF-32
```
When working with character data types in C++, you can use the corresponding literals to represent character constants. For `char`, use single quotes (e.g., `'A'`), for `wchar_t`, use the `L` prefix followed by single quotes (e.g., `L'あ'`), for `char16_t`, use the `u` prefix (e.g., `u'\u1F600'`), and for `char32_t`, use the `U` prefix (e.g., `U'\U0001F600'`).

### String
#### `std::string` 
The `std::string` type in C++ is a class provided by the C++ Standard Library that represents a sequence of characters. It is essentially an object-oriented alternative to the traditional C-style character arrays (null-terminated character arrays). The `std::string` class offers many useful functions and features that simplify working with strings, making them more convenient and safe to use compared to character arrays.

To use `std::string`, you need to include the `<string>` header in your program:
```cpp
#include <iostream>
#include <string>

int main() {
    std::string name = "John Doe";
    std::string greeting = "Hello, ";

    std::cout << greeting << name << "!" << std::endl;

    return 0;
}
```
In this example, we declare and initialize two `std::string` variables, `name` and `greeting`. We then print the resulting greeting string to the console.

#### `std::string_view`
`std::string_view` is a C++ class template (you will learn about templates in the OOP module) that provides a lightweight, read-only view into a sequence of characters. It is defined in the `<string_view>` header and is part of the C++17 standard library.

Here's how you can create a `std::string_view` object:
```cpp
#include <string_view>
#include <iostream>

int main() {
    std::string_view sv("Hello, world!");
    std::cout << sv << std::endl; // Output: "Hello, world!"
    return 0;
}
```
In this example, we create a `std::string_view` object called `sv` that points to a string literal `"Hello, world!"`. We then use the `std::cout` object to display the value of `sv`.

One of the main benefits of using `std::string_view` is that it allows you to avoid unnecessary string copies and allocations. Instead of creating a new `std::string` object to hold a string, you can use a `std::string_view` to provide a view into an existing string.

## Variables
In C++, variables play a crucial role as they are used to store data throughout the program's execution. Variables allow you to store, manipulate, and retrieve data values, enabling the program to perform calculations, make decisions, and process user input. Each variable has a specific data type (e.g., int, float, char, bool) that dictates the kind of data it can store, as well as the amount of memory allocated for it. By giving variables meaningful names and initializing them upon declaration, you can create well-structured and maintainable code that effectively handles the data and logic required for your program's functionality. 

> **Best practice**
>
> In C++, it is considered a best practice to initialize your variables when you declare them. Initializing variables upon creation helps to avoid unintended behavior that may arise from using uninitialized variables, which can contain "garbage" or undefined values. By initializing variables with appropriate initial values, you can ensure your program's stability and predictability.

In C++, there are several ways to define and initialize multiple primitive variables, either of the same data type or different data types.

### Example of Variables
Here's a simple C++ program that demonstrates defining and initializing various primitive data types, followed by an explanation of the program:

<iframe style='max-width:100%; border: 1px solid black; height: 600px; width: 1100px;' height=600 width=1100 src=https://www.interviewbit.com/embed/snippet/4b46d120bac6ccbdc6f4 title='Interviewbit Ide snippet/4b46d120bac6ccbdc6f4' loading="lazy" allow="clipboard-write" allowfullscreen referrerpolicy="unsafe-url" sandbox="allow-scripts allow-same-origin allow-popups allow-top-navigation-by-user-activation allow-popups-to-escape-sandbox"></iframe>

Explanation:

1. The program begins with the inclusion of the `iostream` header file, which provides facilities for input and output operations.

2. The `main` function is the entry point of the program.

3. Inside the `main` function, we define and initialize several primitive data types:
    * Two integer variables (`age` and `year`) with values 25 and 2023, respectively.
    * Two floating-point variables (`temperature` and `pi`) with values 21.5 and 3.141592653589793, respectively. Note that the `temperature` variable is of type `float`, while `pi` is of type `double`.
    * A character variable (`initial`) with the value `'A'`.
    * A boolean variable (`is_active`) with the value `true`.
    * A string variable (`text`) with the value `"Hello, world!"`.
4. We use `std::cout` and the stream insertion operator (`<<`) to print the values of the variables to the console, along with descriptive text for each variable. For the boolean variable `is_active`, we use a ternary conditional operator (`? :`) to print `"Yes"` if the value is `true` and `"No"` otherwise.
5. The program returns 0, indicating successful execution.

When you run this program, it will display the values of the defined and initialized variables on the console. You can make changes to the program and run it again to see how the output changes. If you type inside the editor, it will provide real-time syntax highlighting, making it easy to spot any errors. When you're ready to test your code, click the "Run" button to compile and execute it against a set of sample test cases. If your code encounters any errors or issues, the compiler will display relevant feedback below the editor. You can make the necessary adjustments and rerun your code until it is successfully run.

### `const`
In C++, the `const` keyword is used to indicate that a variable or member function cannot be modified. Here are some examples of using const in C++:
```cpp
#include <iostream>

int main() {
    const int x = 5; // declare a const variable

    // x = 6; // If this line is uncommented, it will cause a compiler error. Try it!

    std::cout << "x = " << x << std::endl;

    return 0;
}
```
In this example, we declare a `const` variable called `x` and initialize it to the value 5. We then try to modify the value of `x`, which will cause a compiler error because `x` is declared as `const`. Finally, we print the value of `x` to the console.

### Uninitialized Variables
In C++, uninitialized variables can contain garbage data. Garbage data is any random or unknown value that may have been previously stored in the memory location where the uninitialized variable is stored. This can happen when the variable is allocated on the stack, heap or global memory.

Garbage data can cause unpredictable behavior in a program if the variable is used before it's properly initialized. In some cases, the value of the uninitialized variable may appear to be valid or meaningful, leading to hard-to-find bugs.

For example, consider the following code:
```cpp
int x;
std::cout << x << std::endl;
```
In this case, `x` is uninitialized, so it contains garbage data. When we try to print the value of `x`, the program will print whatever garbage data happens to be stored in the memory location where `x` is located. This can be any random value, and it can change every time the program runs. To avoid this, we should always initialize `x` before using it:
```cpp
int x = 0;
std::cout << x << std::endl;
```
In this case, `x` is initialized to 0, so when we print its value, we know exactly what it will be.

### Defining and initializing multiple variables of the same data type
#### Single statement with comma-separated variable names and initial values
You can define and initialize multiple variables of the same data type in a single statement by separating the variable names and their initial values with commas.
```cpp
int age1 = 25, age2 = 30, age3; // Declares three integer variables, and initializes two of them
float x = 3.5, y = 4.2, z = 5.8;    // Declares and initializes three float variables
```
Alternatively, you can define and initialize each variable in a separate statement. This method makes the code easier to read and understand, especially when each variable has a different initial value or purpose.
```cpp
int age1 = 25;
int age2 = 30;
int age3;

float x = 3.5;
float y = 4.2;
float z = 5.8;
```

> **Best practice**
>
> Defining and initializing multiple variables in a single line (not recommended)!
>
> Although it's possible to define and initialize multiple variables with different data types in a single line, doing so can make the code harder to read and maintain. This approach is not recommended, but it can be done as follows:
> ```cpp
> int count = 10; double price = 19.99; char letter = 'A'; bool is_valid = true;
> ```

<details>
<summary>List-initialization</summary>
List-initialization, also known as uniform initialization or brace initialization, is a method of initializing variables in C++ using curly braces `{}`. Introduced in C++11, list initialization provides a consistent syntax for initializing objects of different types and can help prevent narrowing conversions that might cause data loss (when you convert a value of one type to a value of another type, and the destination type does not have enough capacity to represent the source value accurately). List-initialization can be used with built-in types, user-defined types, and even containers.

Example:
```cpp
int number1{42};                // List initialization for an int
double number2{3.14};           // List initialization for a double
std::string text{"Hello, C++"}; // List initialization for a std::string
```
In this example, we use list initialization to declare and initialize variables of various types. The `number1` and `number2` variables are initialized with integer and floating-point values, respectively. The `text` variable is initialized with a string value.
</details>

