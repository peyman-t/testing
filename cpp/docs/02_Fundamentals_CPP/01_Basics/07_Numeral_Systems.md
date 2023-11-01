## Numeral systems
Numeral systems are different ways of representing numbers using different symbols or digits. The most common numeral systems used in computing are decimal, binary, hexadecimal, and octal. Here's an overview of each of these systems:

### Decimal System
This is the most familiar numeral system, and it uses 10 digits (0-9) to represent numbers. Each digit in a decimal number represents a power of 10. For example, the number 1234 in decimal system represents `1*10^3 + 2*10^2 + 3*10^1 + 4*10^0`.

### Binary System
This system uses 2 digits (0 and 1) to represent numbers. Each digit in a binary number represents a power of 2. For example, the number 1011 in binary system represents `1*2^3 + 0*2^2 + 1*2^1 + 1*2^0`, which is equivalent to decimal number 11.

### Hexadecimal System
This system uses 16 digits (0-9 and A-F) to represent numbers. Each digit in a hexadecimal number represents a power of 16. For example, the number 3F in hexadecimal system represents `3*16^1 + 15*16^0`, which is equivalent to decimal number 63.

### Octal System
This system uses 8 digits (0-7) to represent numbers. Each digit in an octal number represents a power of 8. For example, the number 35 in octal system represents `3*8^1 + 5*8^0`, which is equivalent to decimal number 29.

In C++, you can display numbers in different numeral systems using the `cout` object from the `iostream` library. Here are some examples:
```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
    int num = 1234;
    
    // Display num in decimal system
    cout << "Decimal: " << num << endl;
    
    // Display num in binary system
    cout << "Binary: " << bitset<12>(num) << endl;
    
    // Display num in hexadecimal system
    cout << "Hexadecimal: " << hex << num << endl;
    
    // Display num in octal system
    cout << "Octal: " << oct << num << endl;
    
    return 0;
}
```
In this example, we define an integer variable `num` with value 1234. We then use the `cout` object to display the value of `num` in decimal, binary, hexadecimal, and octal systems.

To display `num` in binary system, we use the `bitset` template from the `bitset` library to convert the decimal number to binary representation. We specify the width of the binary representation as 10, which ensures that the output contains at least 10 digits, even if the binary representation of `num` requires fewer digits.

To display `num` in hexadecimal system, we use the `hex` manipulator to set the output stream to hexadecimal mode. This allows the subsequent output to be displayed in hexadecimal format.

To display `num` in octal system, we use the `oct` manipulator to set the output stream to octal mode. This allows the subsequent output to be displayed in octal format.