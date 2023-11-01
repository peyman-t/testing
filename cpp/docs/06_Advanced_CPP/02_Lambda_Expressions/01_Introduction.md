## Introduction to Lambda Expressions (C++11 onwards)
### Syntax and Structure of Lambda Expressions
#### Understanding the Lambda Expression Syntax
While the syntax presented captures the general structure of a lambda, it's essential to understand that lambdas offer flexibility in their definition, and not all parts are mandatory in every lambda expression. A lambda expression has the following syntax:
```cpp
[capture clause](parameters) mutable exception_specification -> return_type { body }
```

The different components of a lambda expression include:

* **Capture Clause**: Specifies which outside variables are available for the lambda. The manner of capture (by value, by reference, or a mix) can vary, and we'll delve deeper into this topic subsequently.
* **Parameters**: Just like regular functions, lambdas can accept parameters. This section defines the input the lambda will take.
* **Mutable Specifier**: An optional keyword. If present, it indicates that the lambda has the permission to alter the values of captured variables.
* **Exception Specification**: This is an optional part that dictates which exceptions the lambda might throw.
* **Return Type**: Indicates the type of value the lambda will return. While it's optional and often deduced from the lambda's body, there are scenarios where it might be necessary to specify it explicitly.
* **Body**: Contains the statements that get executed when the lambda is invoked.

Remember, the actual syntax you'll use for a lambda will often be simpler, as you'll only include the parts that are relevant to your specific use case.

#### Capture modes
The capture clause of a lambda expression is used to capture variables from the enclosing scope. There are three ways to capture variables: by value, by reference, and by a default capture mode.

##### By Copy
To capture variables by copy, you can use the following syntax:
```cpp
[=](parameters) mutable -> return_type { body }
```
This captures all variables from the enclosing scope by value. The values of the captured variables are copied into the lambda expression and can be modified if the lambda expression is declared as mutable.

##### By Reference
To capture variables by reference, you can use the following syntax:
```cpp
[&](parameters) mutable -> return_type { body }
```
This captures all variables from the enclosing scope by reference. The lambda expression can modify the values of the captured variables directly.

##### Default Capture Mode
The default capture mode is used when you want to capture some variables by value and others by reference. To specify the default capture mode, you can use the following syntax:
```cpp
[&value1, value2, ...](parameters) mutable -> return_type { body }
```
This captures `value1` by reference and `value2` and other variables by copy.

### Examples of Lambda Expressions with Various Capture Modes
Let's take a look at some examples of lambda expressions with different capture modes:
```cpp
#include <iostream>

int main() {
  int x = 10;
  int y = 20;

  auto lambda1 = [=]() {
    std::cout << "x + y = " << x + y << std::endl;
  };

  auto lambda2 = [&]() {
    x++;
    y++;
    std::cout << "x = " << x << ", y = " << y << std::endl;
  };

  lambda1();
  lambda2();

  std::cout << "x = " << x << ", y = " << y << std::endl;

  return 0;
}
```
In this example, we define two lambda expressions, `lambda1` and `lambda2`. `lambda1` captures `x` and `y` by copy, while `lambda2` captures `x` and `y` by reference. `lambda1` simply prints the sum of `x` and `y`, while `lambda2` increments `x` and `y` and then prints their values. Finally, we call both lambda expressions and print the values of `x` and `y` again.

#### What happens if the “[]” is used instead of “[=]”?

The `[]` in a lambda function's capture clause means that no variables from the enclosing scope are captured. This means that the lambda function cannot access any variables from outside its body.

If you replace `[=]` with `[]` in `lambda1`, you'll get a compilation error. This is because `lambda1` tries to access the variables `x` and `y` from the enclosing scope, but with `[]`, it's not allowed to do so.

#### What happens if one tries to modify “x” and/or “y” in the body of `lambda1`?

The `[=]` capture clause means that all variables from the enclosing scope are captured by value. This means that the lambda function gets its own copy of the variables and does not modify the original variables from the enclosing scope.

If you try to modify `x` or `y` inside `lambda1`, you'll get a compilation error. This is because by default, variables captured by value are `const` within the lambda body. To modify them, you'd need to add the `mutable` keyword to the lambda's declaration, like so:

```cpp
auto lambda1 = [=]() mutable {
    x++;
    y++;
    std::cout << "x + y = " << x + y << std::endl;
};
```
However, even with the `mutable` keyword, the modifications to `x` and `y` inside `lambda1` will only affect the copies of `x` and `y` that the lambda has captured by value. The original `x` and `y` in the `main` function will remain unchanged.

## Using Lambda Expressions with STL Algorithms
The Standard Template Library (STL) in C++ provides a set of powerful algorithms that operate on containers. These algorithms can be used with lambda expressions to provide flexible and efficient solutions to a wide variety of programming problems.

### Overview of Using Lambda Expressions as Predicates and Comparators
Lambda expressions can be used as predicates and comparators with STL algorithms. A predicate is a function that takes an argument and returns a Boolean value. It is used to test elements of a container for a certain condition. A comparator is a function that takes two arguments and returns a Boolean value. It is used to compare elements of a container to determine their relative ordering.

### Examples of Using Lambda Expressions with Algorithms 
#### Example 1: Using Lambda Expressions with `for_each` Algorithm
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
  std::vector<int> v = {1, 2, 3, 4, 5};
  std::for_each(v.begin(), v.end(), [](int n){
    std::cout << n << " ";
  });

  return 0;
}
```
In this example, we use the `for_each` algorithm to iterate over the elements of a vector `v` and print them to the console using a lambda expression. The lambda expression takes an integer argument `n` and prints it to the console.

#### Example 2: Using Lambda Expressions with `find_if` Algorithm
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
  std::vector<int> v = {1, 2, 3, 4, 5};
  auto it = std::find_if(v.begin(), v.end(), [](int n){
    return n > 3;
  });

  if (it != v.end()) {
    std::cout << "First element greater than 3 is: " << *it << std::endl;
  } else {
    std::cout << "No element greater than 3 found!" << std::endl;
  }

  return 0;
}
```
In this example, we use the `find_if` algorithm to find the first element in a vector `v` that is greater than 3 using a lambda expression. The lambda expression takes an integer argument `n` and returns a Boolean value indicating whether `n` is greater than 3.

#### Example 3: Using Lambda Expressions with `remove_if` Algorithm
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
  std::vector<int> v = {1, 2, 3, 4, 5};
  v.erase(std::remove_if(v.begin(), v.end(), [](int n){
    return n % 2 == 0;
  }), v.end());

  for (auto i : v) {
    std::cout << i << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we use the `remove_if` algorithm to remove all even numbers from a vector `v` using a lambda expression. The lambda expression takes an integer argument `n` and returns a Boolean value indicating whether `n` is even. The `remove_if` algorithm moves all the elements that satisfy the condition to the end of the vector and returns an iterator to the first such element. We then use the `erase` method to remove all the elements from the first such element to the end of the vector. Then, the code prints the elements of the updated vector.

#### Example 4: Using Lambda Expressions with Sort Algorithm
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

int main() {
    std::vector<std::string> v = {"apple", "banana", "cherry", "date", "elderberry"};
    std::sort(v.begin(), v.end(), [](const std::string& a, const std::string& b){
        return a.length() < b.length();
    });

    for (auto s : v) {
        std::cout << s << " ";
    }
    std::cout << std::endl;

    return 0;
}
```
In this example, we use the `sort` algorithm to sort a vector `v` of strings in ascending order of length using a lambda expression. The lambda expression takes two arguments of type `const std::string&` and returns a Boolean value indicating whether the first string is less than the second string based on their lengths. Then, the code prints the elements of the updated vector.

#### Example 5: Using Lambda Expressions with Transform Algorithm
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

int main() {
    std::vector<std::string> v = {"apple", "banana", "cherry", "date", "elderberry"};
    std::vector<int> lengths(v.size());
    std::transform(v.begin(), v.end(), lengths.begin(), [](const std::string& s){
        return s.length();
    });

    for (auto i : lengths) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}
```
In this example, we use the `transform` algorithm to create a new vector `lengths` that contains the lengths of the strings in a vector `v` using a lambda expression. The lambda expression takes a string argument `s` and returns the length of the string.

## Lambda Expressions and Function Objects (functors)
### Comparison of lambda expressions and functors
A functor is a class that behaves like a function. Functors are used in C++ to provide a way to encapsulate a set of operations that can be applied to a set of data. A lambda expression is a lightweight alternative to a functor that can be defined inline. Both lambda expressions and functors can be used as function objects in C++, which means that they can be passed to algorithms that expect a function object as an argument.

Lambda expressions are more concise and easier to define than functors, but they have some limitations. For example, lambda expressions cannot have stateful template parameters, which means that they cannot be used as template arguments in certain cases. Functors, on the other hand, can have stateful template parameters.

### When to Use Lambda Expressions and When to Use Functors
Lambda expressions are generally preferred over functors when the function object is only used in one place and does not require any complex state or behavior. Functors are generally preferred over lambda expressions when the function object requires complex state or behavior, or when the function object is used in multiple places.

### Converting Lambda Expressions to Function Objects (`std::function`)
Lambda expressions can be converted to function objects using the `std::function` template class. The `std::function` class provides a type-erased wrapper around a function object that allows it to be stored, copied, and invoked like any other object. 

A type-erased wrapper refers to an object that can hold and manage any callable entity (like functions, lambda expressions, or functors) regardless of their specific type, while presenting a unified interface. In essence, it "erases" the specific type details of the callable entity, allowing different callables to be treated in a uniform manner. The `std::function` class achieves this by internally using polymorphism and dynamic memory allocation to handle the different types of callable entities it might wrap.

Here's an example:
```cpp
#include <iostream>
#include <functional>

int main() {
  auto lambda = [](int x, int y) {
    return x + y;
  };

  std::function<int(int, int)> func = lambda;

  std::cout << "lambda(2, 3) = " << lambda(2, 3) << std::endl;
  std::cout << "func(2, 3) = " << func(2, 3) << std::endl;

  return 0;
}
```
In this example, we define a lambda expression `lambda` that takes two integers as arguments and returns their sum. We then create a `std::function` object `func` that takes two integers as arguments and returns an integer, and initialize it with the lambda expression. We can then call the lambda expression and the `std::function` object using the same syntax.