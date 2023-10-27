## Program Structure 

A C++ program structure typically consists of a series of essential elements that make it functional, organized, and easy to understand. These elements include preprocessor directives, comments, the main function, input and output, variables, loops, and control structures. In this text, we will elaborate on these elements using simple examples.

### Comments
Comments are an essential part of the program structure, as they help explain the code and improve readability. In C++, single-line comments start with //, while multi-line comments are enclosed between /* and */. For example:

```cpp
// This is a single-line comment

/* This is a
   multi-line
   comment */

```

> **Best practice:**
> 
> Generously use comments in your code, and compose them as though addressing someone who lacks any understanding of the code's purpose. Refrain from presuming that you will recall the rationale behind particular decisions.
> Adding to this idea, incorporating descriptive comments not only benefits your future self but also makes your code more maintainable and accessible to others. Detailed comments can save time and effort during the debugging process, as they provide a clear understanding of the code's intent and functionality. Additionally, well-documented code facilitates collaboration, as it allows other developers to quickly grasp the purpose of the code and make necessary modifications without having to decipher the underlying logic.


### Preprocessor Directives
Preprocessor directives are an essential aspect of C++ programming, as they instruct the preprocessor to perform specific actions before the program is compiled. The preprocessor is a separate processing stage that occurs before the actual compilation. It manipulates the source code based on these directives and generates a modified source code as output, which is then passed to the compiler.

Here are some common preprocessor directives in C++:

#### `#include` 
This directive is used to include header files that contain declarations, definitions, and macros needed in the program. Header files can be either standard libraries provided by the C++ Standard Library (such as iostream, vector, or string) or user-defined headers. The `#include` directive can use angle brackets (`<>`) for standard libraries and double quotes (`""`) for user-defined headers. For example:

```cpp
#include <iostream> // Includes the standard iostream library for input and output operations
#include "myHeader.h" // Includes a user-defined header file named myHeader.h
```

When the `#include` directive is written as `#include <header_file>`, the compiler searches for the header file in the standard system directories. For example, on a Unix-based system, the compiler might search in directories like `/usr/include` or `/usr/local/include`. On a Windows system with MinGW, it might search in directories like `C:\MinGW\include`.

When the `#include` directive is written as `#include "header_file"`, the compiler searches for the header file in the current directory or project directory first. If the header file is not found in the current directory, the compiler continues the search in additional directories specified by the compiler's search path configuration. These additional directories may include standard system directories, user-defined directories, or directories specified by command-line options.

It's important to note that the specific directories searched for header files can vary depending on the development environment, operating system, and compiler settings. The examples provided above illustrate common directories, but the actual directories may differ based on your specific setup.

#### `#define`
The `#define` directive in C++ is used to create symbolic constants and macros. It allows you to define identifiers that can be replaced with specific values or expressions during the preprocessing stage. Here are some important points to consider:

- **Symbolic Constants:** With `#define`, you can define symbolic constants that represent fixed values or expressions. These constants are not variables and do not occupy memory at runtime. They act as placeholders that the compiler replaces with their respective values during preprocessing. For example:

  ```cpp
  #define PI 3.14159 // Defines a symbolic constant named PI with the value 3.14159
  ```

- **Macros:** The `#define` directive can also be used to define macros, which are essentially preprocessor functions. Macros are like "find-and-replace" operations performed by the compiler before the actual compilation takes place. By convention, macro names are often written in uppercase letters to distinguish them from regular variables and functions.

- **Macro Parameters:** Macros can accept parameters that are enclosed in parentheses. These parameters are placeholders for values that you can provide when using the macro. It is important to enclose the macro parameters in parentheses within the macro definition to ensure proper expansion and avoid unexpected results. For example:

  ```cpp
  #define SQUARE(x) ((x) * (x)) // Defines a macro that calculates the square of a value
  ```

- **Compiler Processing of Macros:** It is important to understand that macros are processed by the compiler as simple text substitutions during the preprocessing stage. When a macro is used in the code, the compiler replaces the macro with its corresponding definition. This "find-and-replace" nature of macros can be better understood with an example:

  ```cpp
  #define MAX(a, b) ((a) > (b) ? (a) : (b)) // Defines a macro that returns the maximum of two values

  int x = 5;
  int y = 8;
  int maxVal = MAX(x, y); // Expands to: ((x) > (y) ? (x) : (y))
  ```
  In this example, the macro `MAX(x, y)` is expanded by the compiler to the expression `((x) > (y) ? (x) : (y))`. It effectively replaces `MAX(x, y)` with the code that compares `x` and `y`, returning the maximum value.


<details>
<summary>Advanced preprocessor directives</summary>

#### `#undef`
This directive is used to remove a defined macro, allowing it to be redefined later in the code. For example:

```cpp
#define PI 3.14159
#undef PI // Undefines the macro PI
#define PI 3.14 // Redefines the macro PI with a new value
```

#### Conditional Directives
Conditional directives in C++ are used to control which parts of the code are processed and compiled based on certain conditions. They allow you to include or exclude specific code blocks depending on whether certain conditions are met. The most commonly used conditional directives are `#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, and `#endif`. Here's an example:

```cpp
#define DEBUG_MODE
```

In this example, a macro named `DEBUG_MODE` is defined using the `#define` directive. This macro serves as a conditional flag that can be used to enable or disable certain code sections.

```cpp
#ifdef DEBUG_MODE
    std::cout << "Debug mode is active" << std::endl;
#else
    std::cout << "Debug mode is not active" << std::endl;
#endif
```

The `#ifdef` directive checks whether the macro `DEBUG_MODE` has been defined. If it has been defined, the code block between `#ifdef` and `#else` (or `#endif` if there's no `#else`) is included during compilation. In this case, the message "Debug mode is active" is printed to the console.

If `DEBUG_MODE` has not been defined, the code block following `#else` (if present) is included instead. In the provided example, the message "Debug mode is not active" is printed when `DEBUG_MODE` is not defined.

The `#endif` directive marks the end of the conditional block, ensuring that the correct sections of code are processed based on the condition.

Conditional directives are commonly used to enable or disable certain features, customize the behavior of a program, or handle different configurations for development and production environments. By selectively including or excluding code based on conditions, you can create more flexible and maintainable codebases.

It's worth noting that the example above demonstrates a simple case where the `DEBUG_MODE` macro is manually defined. In practice, the conditional directives are often used in conjunction with build configurations, compiler options, or other preprocessor macros to control the behavior of the code at compile time.

Remember that conditional directives are processed by the preprocessor and do not have any impact on the runtime behavior of the program. They allow you to tailor the compilation process and code generation based on specific conditions, resulting in more versatile and adaptable programs.

#### `#pragma`
This directive is used to issue special commands to the compiler, which are implementation-specific. For example, the `#pragma` once directive ensures that a header file is included only once in the program, preventing multiple inclusions:

```cpp
#pragma once
// The rest of the header file
```
It's important to note that the `#pragma once` directive is specific to the header file in which it is seen by the preprocessor. It ensures that the particular header file is included only once in the translation unit where it is encountered.
</details>


### The `main` function
The `main` function in C++ serves as the entry point of the program. When a C++ program is executed, the `main` function is called first, and it initiates the program's execution. The `main` function typically contains the primary logic and flow control of the program, and it's responsible for coordinating other functions and tasks. The `main` function has a specific structure, and its return type is typically an integer, indicating the program's exit status.

Here's the structure of the main function in C++:

```cpp
int main() {
    // Program code goes here
    return 0;
}
```

The `int` before `main` indicates that the function returns an integer value, and `return 0;` signifies that the program executed successfully. The pair of parentheses `()` after the function's name signifies that it takes no arguments.

<details>
<summary>Input arguments of `main()`</summary>
The `main` function can also take command-line arguments if required, using the following structure:

```cpp
int main(int argc, char* argv[]) {
    // Program code goes here
    return 0;
}
```
In this case, `argc` is an integer representing the number of command-line arguments passed to the program, including the program's name itself, while `argv` is an array of character pointers, each pointing to a null-terminated string representing the command-line arguments. Since this depends on the variable and data types section of the course that is covered later, you can return to this when you have studied that section.
</details>

### Input and Output
C++ uses the `std::cin` and `std::cout` objects, which are part of the `iostream` library, for input and output operations. For example:

```cpp
#include <iostream>

int main() {
    int number;
    std::cout << "Enter a number: ";
    std::cin >> number;
    std::cout << "You entered: " << number << std::endl;
    return 0;
}
```
