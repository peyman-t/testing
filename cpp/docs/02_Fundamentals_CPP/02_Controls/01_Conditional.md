## Control Structures

Control structures are essential building blocks of any programming language, as they allow you to control the flow of a program. In this text, we'll discuss fundamental control structures in C++.

## If-Else Statements

In C++, `if-else` statements are used to make decisions based on the value of a Boolean expression. The `if` statement checks whether a condition is `true` or `false`, and executes a block of code if the condition is true. The `else` statement is used to execute a different block of code if the condition is false. The basic syntax of the `if-else` statement in C++ is as follows:
```cpp
if (condition) {
    // Code to execute if the condition is true
}
```
In this code block, the `if` statement is used to check whether a given `condition` is true or false. If the `condition` is true, the block of code inside the curly braces `{}` is executed. If the condition is false, the block of code is skipped.

```cpp
if (condition) {
    // Code to execute if the condition is true
} else {
    // Code to execute if the condition is false
}
```
In this code block, the `if` statement is used to check whether a given `condition` is true or false. If the `condition` is true, the block of code inside the first set of curly braces `{}` is executed. If the `condition` is false, the block of code inside the `else` statement is executed.

```cpp
if (condition) {
    // Code to execute if the condition is true
} else if (condition2) {
    // Code to execute if the condition2 is true
} else {
    // Code to execute if condition and condition2 are false
}
```
In this code block, the `if-else-if-else` statement is used to check multiple conditions in a sequence. The first if statement is used to check whether a given `condition` is true or false. If the `condition` is true, the block of code inside the first set of curly braces `{}` is executed. If the `condition` is false, the program proceeds to the next `else if` statement, which checks whether a second `condition2` is true or false. If the second condition is true, the block of code inside the second set of curly braces `{}` is executed. If both conditions are false, the program executes the `else` statement and the block of code inside the third set of curly braces `{}` is executed.

Here's an example that demonstrates the use of an if-else statement:

```cpp
#include <iostream>

int main() {
    int number = 42;

    if (number == 0) {
        std::cout << "The number is zero." << std::endl;
    } else if (number % 2 == 0) {
        std::cout << "The number is even." << std::endl;
    } else {
        std::cout << "The number is odd." << std::endl;
    }

    return 0;
}
```
The first `if` statement checks whether the value of `number` is `0`. If the condition is true, the program outputs the message `The number is zero.` to the console. If the condition is false, the program proceeds to the next `else if` statement, which checks whether `number` is even. If the condition is true, the program outputs the message `The number is even.` to the console. If the second condition is also false, the program executes the `else` statement and outputs the message `The number is odd.` to the console. Since `number` is initialized to 42, the condition `number % 2 == 0` is true, so `The number is even.` is printed.

### Nested If-Else Statements
In C++, it is possible to nest `if-else` statements inside other `if-else` statements to create more complex decision-making structures. Here's an example of a nested `if-else` statement in C++:
```cpp
#include <iostream>

using namespace std;

int main() {
    int x = 15, y = 20;
    if (x > 10) {
        if (y > 15) {
            cout << "x is greater than 10 and y is greater than 15" << endl;
        }
        else {
            cout << "x is greater than 10 but y is less than or equal to 15" << endl;
        }
    }
    else {
        cout << "x is less than or equal to 10" << endl;
    }
    return 0;
}
```
In this example, we have declared two integer variables `x` and `y` and assigned them the values of `15` and `20`, respectively. We have then used nested `if-else` statements to check whether `x` is greater than `10` and `y` is greater than `15`. If both conditions are true, the program outputs the message `x is greater than 10 and y is greater than 15`. If the first condition is true but the second is false, the program outputs the message `x is greater than 10 but y is less than or equal to 15`. If the first condition is false, the program outputs the message `x is less than or equal to 10`. Since `x = 15` and `y = 20`, the message `x is greater than 10 and y is greater than 15` is printed.

## Switch-Case Statements
In C++, the `switch` statement is used to perform different actions based on the value of a variable or an expression. The `switch` statement is often used as an alternative to a series of `if-else` statements. The basic syntax of the `switch` statement in C++ is as follows:
```cpp
switch (expression) {
    case constant1:
        // code to be executed if expression == constant1
        break;
    case constant2:
        // code to be executed if expression == constant2
        break;
    default:
        // code to be executed if expression is not equal to any of the constants
        break;
}
```
The `expression` is evaluated, and the value is compared to each of the `constant` values. If the value of the `expression` matches a `constant`, the code block associated with that `constant` is executed. If no match is found, the `default` code block is executed.

The `break` statement is used to exit the `switch` statement and continue executing the code after the `switch` statement.


Here's an example that demonstrates the use of a switch-case statement:

```cpp
#include <iostream>

int main() {
    int day;

    std::cout << "Enter a number between 1 and 7 representing the day of the week: ";
    std::cin >> day;

    switch (day) {
        case 1:
            std::cout << "Monday" << std::endl;
            break;
        case 2:
            std::cout << "Tuesday" << std::endl;
            break;
        case 3:
            std::cout << "Wednesday" << std::endl;
            break;
        case 4:
            std::cout << "Thursday" << std::endl;
            break;
        case 5:
            std::cout << "Friday" << std::endl;
            break;
        case 6:
            std::cout << "Saturday" << std::endl;
            break;
        case 7:
            std::cout << "Sunday" << std::endl;
            break;
        default:
            std::cout << "Invalid input. Please enter a number between 1 and 7."
            std::endl;
    }

    return 0;
}
```
This code prompts the user to enter a number between 1 and 7 to represent a day of the week. It then uses a switch statement to output the corresponding day of the week to the console. If the `day` variable is `1`, the program outputs `Monday`. If the `day` variable is `2`, the program outputs `Tuesday`, and so on. If the `day` variable does not match any of the cases, the `default` block is executed, and the program outputs a message to the console indicating that the input is invalid.

When the `break` statement is not used for a case in a switch-case construct, it results in a fall-through behavior. This means that once a matching case is executed, the control flow continues to the next case, executing its code as well, and so on until a `break` statement is encountered or the end of the switch block is reached.

Here's an example to illustrate the behavior when `break` is not used for a case:

```cpp
#include <iostream>

int main() {
    int num = 2;

    switch (num) {
        case 1:
            std::cout << "Case 1" << std::endl;
        case 2:
            std::cout << "Case 2" << std::endl;
        case 3:
            std::cout << "Case 3" << std::endl;
        default:
            std::cout << "Default case" << std::endl;
    }

    return 0;
}
```

In this example, the value of `num` is `2`. The switch-case construct compares `num` against each case. Since `num` matches the "case 2" label, the code block under that case is executed, and "Case 2" is printed to the console.

However, because there is no `break` statement after the "case 2" code block, the control flow falls through to the next case, which is "case 3". Consequently, the code block under "case 3" is also executed, and "Case 3" is printed to the console.

After executing the code block of "case 3", since there is no `break` statement there either, the control flow falls through to the "default" case. The code block under the `default` label is executed, and "Default case" is printed to the console.

The output of this example would be:

```
Case 2
Case 3
Default case
```

This fall-through behavior can be intentionally utilized when you want multiple cases to execute the same code block. However, it is crucial to document and design the switch-case construct carefully to avoid unintended execution or logical errors when fall-through behavior is not desired.