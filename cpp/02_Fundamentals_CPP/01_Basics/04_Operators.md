
## Operators

Operators are symbols used in C++ to perform various operations on operands. In other words, an operator is a symbol that tells the compiler to perform specific mathematical or logical operations on one or more operands. C++ has a wide range of operators, including arithmetic, relational, logical, assignment, and bitwise operators.

### Arithmetic Operators
Arithmetic operators are used to perform mathematical operations such as addition, subtraction, multiplication, division, and modulo on operands. The following are some examples of arithmetic operators in C++:

```cpp
int x = 10, y = 5, result;
result = x + y;  // Addition
result = x - y;  // Subtraction
result = x * y;  // Multiplication
result = x / y;  // Division
result = x % y;  // Modulo
```
In the above example, `x` and `y` are operands, and `+`, `-`, `*`, `/`, and `%` are arithmetic operators.

Example program:
```cpp
#include <iostream>

using namespace std;

int main() {
    int x = 10, y = 5, result;
    result = x + y; // Addition
    cout << "x + y = " << result << endl;
    result = x - y; // Subtraction
    cout << "x - y = " << result << endl;
    result = x * y; // Multiplication
    cout << "x * y = " << result << endl;
    result = x / y; // Division
    cout << "x / y = " << result << endl;
    result = x % y; // Modulo
    cout << "x % y = " << result << endl;
    return 0;
}
```
In this example, we have declared two integer variables `x` and `y`, and we have assigned them the values of `10` and `5`, respectively. We have then used arithmetic operators `+`, `-`, `*`, `/`, and `%` to perform addition, subtraction, multiplication, division, and modulo (i.e., finding the remainder of division of one number by another) operations on `x` and `y`. Finally, we have displayed the results of these operations using the `cout` statement.

#### `++` and `--` Operators 
The `++` and `--` operators in C++ are used for incrementing and decrementing variables by a value of 1. These operators can be applied to both integer and floating-point types. Let's discuss their usage and the difference between the prefix and postfix versions.

##### Prefix Increment and Decrement (++variable, --variable):
The prefix increment (`++variable`) and decrement (`--variable`) operators first modify the value of the variable and then return the updated value. Here's an example:

```cpp
int x = 5;
int y = ++x;  // Increment x and assign the updated value to y

std::cout << "x: " << x << std::endl;  // Output: 6
std::cout << "y: " << y << std::endl;  // Output: 6
```

In this example, the value of `x` is incremented by 1 before being assigned to `y`. Both `x` and `y` have the updated value of 6.

##### Postfix Increment and Decrement (variable++, variable--):
The postfix increment (`variable++`) and decrement (`variable--`) operators also modify the value of the variable but return the original value before the modification. Here's an example:

```cpp
int x = 5;
int y = x++;  // Assign the value of x to y and then increment x

std::cout << "x: " << x << std::endl;  // Output: 6
std::cout << "y: " << y << std::endl;  // Output: 5
```

In this example, the value of `x` is assigned to `y` before being incremented by 1. The value of `y` remains the original value of `x` (5), while `x` has the updated value of 6.

##### Difference between Prefix and Postfix Versions:
The main difference between the prefix and postfix versions of the `++` and `--` operators is the order in which the increment or decrement operation is performed. The prefix version performs the operation before evaluating the expression, while the postfix version performs the operation after evaluating the expression.

In most cases, the choice between the prefix and postfix versions depends on the desired behavior in a specific context. If you need to use the current value of a variable and then increment or decrement it, the postfix version can be used. On the other hand, if you want to increment or decrement the variable first and then use the updated value, the prefix version is appropriate.

It's important to note that the `++` and `--` operators can be used with variables, but they should be used with caution to ensure code clarity and avoid unintended side effects.

### Relational Operators
Relational operators are used to compare two operands and return a Boolean value (true or false). The following are some examples of relational operators in C++:

```cpp
int x = 10, y = 5;
bool result;
result = x > y;   // Greater than
result = x < y;   // Less than
result = x >= y;  // Greater than or equal to
result = x <= y;  // Less than or equal to
result = x == y;  // Equal to
result = x != y;  // Not equal to
```

In the above example, `x` and `y` are operands, and `>`, `<`, `>=`, `<=`, `==`, and `!=` are relational operators.

Example program:
```cpp
#include <iostream>

using namespace std;

int main() {
    int x = 10, y = 5;
    bool result;
    result = x == y; // Equal to
    cout << "x == y is " << result << endl;
    result = x != y; // Not equal to
    cout << "x != y is " << result << endl;
    result = x > y; // Greater than
    cout << "x > y is " << result << endl;
    result = x < y; // Less than
    cout << "x < y is " << result << endl;
    result = x >= y; // Greater than or equal to
    cout << "x >= y is " << result << endl;
    result = x <= y; // Less than or equal to
    cout << "x <= y is " << result << endl;
    return 0;
}
```
In this example, we have declared two integer variables `x` and `y`, and we have assigned them the values of `10` and `5`, respectively. We have then used relational operators `==`, `!=`, `>`, `<`, `>=`, and `<=` to compare `x` and `y`. Finally, we have displayed the results of these comparisons using the `cout` statement.

### Logical Operators
Logical operators are used to perform logical operations on operands. The following are some examples of logical operators in C++:

``` cpp
bool x = true, y = false, result;
result = x && y;  // Logical AND
result = x || y;  // Logical OR
result = !x;      // Logical NOT
```
In the above example, `x` and `y` are operands, and `&&`, `||`, and `!` are logical operators.

here are the truth tables for AND, OR, and NOT operations combined in one table:

|    A    |    B    | A AND B | A OR B | NOT A |
|---------|---------|---------|--------|-------|
| false   | false   | false   | false  | true  |
| false   | true    | false   | true   | true  |
| true    | false   | false   | true   | false |
| true    | true    | true    | true   | false |

In the above table:

- 'A AND B' is the result of the logical AND operation on inputs A and B.
- 'A OR B' is the result of the logical OR operation on inputs A and B.
- 'NOT A' is the result of the logical NOT operation on input A (Input B is not included because NOT is a unary operation, meaning it works on a single operand).

Example program:
```cpp
#include <iostream>

using namespace std;

int main() {
    bool a = true, b = false, result;
    result = a && b; // Logical AND
    cout << "a && b is " << result << endl;
    result = a || b; // Logical OR
    cout << "a || b is " << result << endl;
    result = !a; // Logical NOT
    cout << "!a is " << result << endl;
    return 0;
}
```
In this example, we have declared two boolean variables `a` and `b`, and we have assigned them the values of `true` and `false`, respectively. We have then used logical operators `&&`, `||`, and `!` to perform logical AND, logical OR, and logical NOT operations on `a` and `b`. Finally, we have displayed the results of these operations using the `cout` statement.

The output of the program would be:
```cpp
a && b is 0
a || b is 1
!a is 0
```
Note that `1` represents `true` and `0` represents `false` in boolean expressions.

### Bitwise Operators
Bitwise operators are used to perform bitwise operations on binary numbers. The following are some examples of bitwise operators in C++:

```cpp
int x = 10, y = 5, result;
result = x & y;   // Bitwise AND
result = x | y;   // Bitwise OR
result = x ^ y;   // Bitwise XOR
result = ~x;      // Bitwise NOT
result = x << y;  // Bitwise left shift
result = x >> y;  // Bitwise right shift
```
In the above example, `x` and `y` are operands, and `&`, `|`, `^`, `~`, `<<`, and `>>` are bitwise operators.

Let's go through each operation one by one. To better visualize the operations, let's first convert the integers into binary:

```
x = 10 -> 1010 in binary
y = 5  -> 0101 in binary
```

1. Bitwise AND (`&`): This operation results in 1 only if both corresponding bits are 1.

```cpp
result = x & y;
```

```
  x = 1010
& y = 0101
-----------
  result = 0000 -> 0 in decimal
```

2. Bitwise OR (`|`): This operation results in 1 if at least one of the corresponding bits is 1.

```cpp
result = x | y;
```

```
  x = 1010
| y = 0101
-----------
  result = 1111 -> 15 in decimal
```

3. Bitwise XOR (`^`): This operation results in 1 only if exactly one of the corresponding bits is 1.

```cpp
result = x ^ y;
```

```
  x = 1010
^ y = 0101
-----------
  result = 1111 -> 15 in decimal
```

4. Bitwise NOT (`~`): This operation inverts the bits (0s become 1s and 1s become 0s).

```cpp
result = ~x;
```

```
  x = 1010
~ x = 0101 -> 5 in decimal
```

Please note that this example assumes 4-bit integers. However, in reality, C++ typically uses 32-bit (for `int` on most modern systems) or 64-bit integers (for `long long`). The NOT operation would result in a large negative number when performed on these integers due to the concept of two's complement used to represent negative numbers in binary. 

5. Bitwise left shift (`<<`): This operation shifts the bits of the number to the left by the number of places specified. It inserts 0s in the new positions on the right.

```cpp
result = x << y;
```

```
  x = 1010
After left shifting 5 positions, we get:

  result = 1010000000 -> 320 in decimal
```

6. Bitwise right shift (`>>`): This operation shifts the bits of the number to the right by the number of places specified. It inserts 0s in the new positions on the left.

```cpp
result = x >> y;
```

```
  x = 1010
After right shifting 5 positions, we get:

  result = 0000 -> 0 in decimal
```
In the above shift operations, we are considering y as the number of shift positions. However, in a typical scenario, shifting more positions than the number of bits a data type holds does not make much sense. So, it's often used with smaller numbers.

Bitwise left shift (`<<`) and bitwise right shift (`>>`) have an arithmetic significance in binary.

1. Bitwise left shift (`<<`): Performing a bitwise left shift on a number is equivalent to multiplying it by 2. Every time you shift the bits of a number one place to the left, you double the number.

For example, let's consider the number 5 (in binary, 0101). If we left shift by 1 (`5 << 1`), we get 10 (in binary, 1010). Hence, `5 << 1` is equivalent to `5 * 2`.

2. Bitwise right shift (`>>`): Performing a bitwise right shift on a number is equivalent to integer division by 2 (ignoring any remainder). Every time you shift the bits of a number one place to the right, you halve the number.

For example, let's consider the number 10 (in binary, 1010). If we right shift by 1 (`10 >> 1`), we get 5 (in binary, 0101). Hence, `10 >> 1` is equivalent to `10 / 2`.

These relations hold true for positive integers. For negative numbers, it depends on how negative numbers are represented (usually it's two's complement) and specific language rules. For bitwise right shift, some languages like C++ do not specify whether it performs an arithmetic (sign-preserving) shift or a logical shift (not sign-preserving), so it's generally advisable to avoid using it with negative numbers.


Example program:
```cpp
#include <iostream>

using namespace std;

int main() {
    unsigned int a = 60; // 0011 1100
    unsigned int b = 13; // 0000 1101
    unsigned int result;
    result = a & b; // Bitwise AND
    cout << "a & b is " << result << endl;
    result = a | b; // Bitwise OR
    cout << "a | b is " << result << endl;
    result = a ^ b; // Bitwise XOR
    cout << "a ^ b is " << result << endl;
    result = ~a; // Bitwise NOT
    cout << "~a is " << result << endl;
    result = a << 2; // Bitwise Left Shift
    cout << "a << 2 is " << result << endl;
    result = a >> 2; // Bitwise Right Shift
    cout << "a >> 2 is " << result << endl;
    return 0;
}
```
In this example, we have declared two `unsigned integer` variables `a` and `b`, and we have assigned them the values of `60` (represented in binary as `0011 1100`) and `13` (represented in binary as `0000 1101`), respectively. We have then used bitwise operators `&`, `|`, `^`, `~`, `<<`, and `>>` to perform bitwise AND, bitwise OR, bitwise XOR, bitwise NOT, bitwise left shift, and bitwise right shift operations on `a` and `b`. Finally, we have displayed the results of these operations using the `cout` statement.

The output of the program would be:
```cpp
a & b is 12
a | b is 61
a ^ b is 49
~a is 4294967235
a << 2 is 240
a >> 2 is 15
```
Note that the bitwise left shift (`<<`) and bitwise right shift (`>>`) operations shift the bits of a number to the left or right by the specified number of positions. For example, `a << 2` shifts the bits of a to the left by two positions, which results in the binary representation `1111 0000`, or the decimal value `240`.

### Assignment Operators
Assignment operators are used to assign a value to a variable. The following are some examples of assignment operators in C++:

```cpp
int x = 10, y = 5;
x += y;   // x = x + y
x -= y;   // x = x - y
x *= y;   // x = x * y
x /= y;   // x = x / y
x %= y;   // x = x % y
x &= y;   // x = x & y
```

In the above example, `x` and `y` are operands, and `+=`, `-=`, `*=`, `/=`, and `%=` are assignment operators.

Example program:
```cpp
#include <iostream>

using namespace std;

int main() {
    int x = 10, y = 5;
    cout << "x = " << x << ", y = " << y << endl;
    x += y; // Addition Assignment
    cout << "x += y is " << x << endl;
    x -= y; // Subtraction Assignment
    cout << "x -= y is " << x << endl;
    x *= y; // Multiplication Assignment
    cout << "x *= y is " << x << endl;
    x /= y; // Division Assignment
    cout << "x /= y is " << x << endl;
    x %= y; // Modulo Assignment
    cout << "x %= y is " << x << endl;
    x &= y; // AND Assignment
    cout << "x &= y is " << x << endl;
    return 0;
}
```
In this example, we have declared two integer variables `x` and `y`, and we have assigned them the values of `10` and `5`, respectively. We have then used assignment operators `+=`, `-=`, `*=`, `/=`, `%=`, and `&=` to modify the value of `x` based on the operation over `x` and `y`. Finally, we have displayed the results of these operations using the `cout` statement.

The output of the program would be:
```cpp
x = 10, y = 5
x += y is 15
x -= y is 10
x *= y is 50
x /= y is 10
x %= y is 0
x &= y is 0
```

### `sizeof`
In C++, the `sizeof` keyword is an operator that returns the size in bytes of its operand. The operand can be a data type, an expression, or a variable. The sizeof operator is evaluated at compile time, which means that it does not cause any runtime overhead.

The `sizeof` operator can be used to determine the size of any data type, including fundamental types such as `int`, `double`, and `char`, as well as user-defined types such as classes, structs, and enums. The size of a data type depends on the implementation and the platform, but is guaranteed to be at least as large as the minimum required by the C++ standard.

Here are some examples of using the `sizeof` operator with different data types:
```cpp
#include <iostream>

int main() {
    int myInt = 42;
    double myDouble = 3.14;
    char myChar = 'a';

    std::cout << "Size of int: " << sizeof(int) << " bytes" << std::endl;
    std::cout << "Size of myInt: " << sizeof(myInt) << " bytes" << std::endl;
    std::cout << "Size of double: " << sizeof(double) << " bytes" << std::endl;
    std::cout << "Size of myDouble: " << sizeof(myDouble) << " bytes" << std::endl;
    std::cout << "Size of char: " << sizeof(char) << " bytes" << std::endl;
    std::cout << "Size of myChar: " << sizeof(myChar) << " bytes" << std::endl;

    return 0;
}
```
In this example, we declare and initialize a few variables of different fundamental data types: an integer `myInt` with value 42, a double `myDouble` with value 3.14, and a character `myChar` with value `'a'`. We then use the `sizeof` operator to determine the size in bytes of each data type, both for the type itself and for the corresponding variable.

The output of this program will be:
```cpp
Size of int: 4 bytes
Size of myInt: 4 bytes
Size of double: 8 bytes
Size of myDouble: 8 bytes
Size of char: 1 bytes
Size of myChar: 1 bytes
```
This shows on the given platform, the size of an integer and a double are both 4 bytes, while the size of a character is only 1 byte. The size of the corresponding variables is the same as the size of the data type.

## List of Operators
Here's a list of all the operators in C++:

| Category | Operator | Description |
| --- | --- | --- |
| Arithmetic | + | Addition |
| | - | Subtraction |
| | * | Multiplication |
| | / | Division |
| | % | Modulo |
| Relational | == | Equal to |
| | != | Not equal to |
| | > | Greater than |
| | < | Less than |
| | >= | Greater than or equal to |
| | <= | Less than or equal to |
| Logical | && | Logical AND |
| | \|\| | Logical OR |
| | ! | Logical NOT |
| Assignment | = | Assignment |
| | += | Addition assignment |
| | -= | Subtraction assignment |
| | *= | Multiplication assignment |
| | /= | Division assignment |
| | %= | Modulo assignment |
| | &= | Bitwise AND assignment |
| | \|= | Bitwise OR assignment |
| | ^= | Bitwise XOR assignment |
| | <<= | Left shift assignment |
| | >>= | Right shift assignment |
| Bitwise | & | Bitwise AND |
| | \| | Bitwise OR |
| | ^ | Bitwise XOR |
| | ~ | Bitwise NOT |
| | << | Left shift |
| | >> | Right shift |
| Ternary | ?: | Conditional operator |
| Scope | :: | Scope resolution operator |
| Member | . | Member selection operator |
| | -> | Member selection through pointer operator |
| Increment/Decrement | ++ | Increment |
| | -- | Decrement |
| Comma | , | Comma operator |

Some operators such as member that are not mentioned here will be discussed in next modules.