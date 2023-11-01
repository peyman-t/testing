## STL Function Objects (Functors)
STL function objects, also known as functors, are objects that behave like functions. They are used extensively in the STL to provide customizable behavior for algorithms, containers, and other components. In this section, we'll cover the basic concepts of function objects in the STL, including their role in the STL, using predefined function objects, creating custom function objects, and using function objects with algorithms and containers.

### Overview of Function Objects and their Role in the STL
Function objects in the STL are objects that behave like functions. They are used extensively in the STL to provide customizable behavior for algorithms, containers, and other components. Function objects are typically implemented as classes that overload the () operator (the function call operator). When an object of the class is called using the () operator, the overloaded function call operator is invoked, allowing the object to behave like a function.

Function objects provide several advantages over traditional function pointers, including the ability to maintain state between calls, the ability to be parameterized with additional data, and the ability to be used with templates.

## Using Predefined Function Objects
The STL provides a set of predefined function objects that can be used with algorithms and containers. These include arithmetic, relational, logical, and bitwise function objects. Here are some examples of using predefined function objects:
```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <functional>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5};

    // Using arithmetic function objects
    std::transform(nums.begin(), nums.end(), nums.begin(),
                   std::bind(std::multiplies<int>(), std::placeholders::_1, 2));

    // Using relational function objects
    auto it = std::find_if(nums.begin(), nums.end(),
                           std::bind(std::greater<int>(), std::placeholders::_1, 4));
    if (it != nums.end()) {
        std::cout << "Found element greater than 4: " << *it << std::endl;
    }

    // Using logical function objects
    bool all_even = std::all_of(nums.begin(), nums.end(),
                                std::not1(std::bind1st(std::modulus<int>(), 2)));
    if (all_even) {
        std::cout << "All elements are even." << std::endl;
    } else {
        std::cout << "Some elements are odd." << std::endl;
    }

    // Using bitwise function objects
    int num = 0b10101010;
    int mask = 0b11110000;
    int masked = std::bit_and<int>()(num, mask);
    std::cout << "Masked number is: " << masked << std::endl;

    return 0;
}
```
Let's delve deeper into the code:

1. Initialization: 
   - A vector named `nums` is initialized with integers from 1 to 5.
   - Two binary numbers, `num` and `mask`, are also defined for later use.

2. Doubling Elements with `std::transform`:
   - The `std::transform` algorithm is employed to iterate over the `nums` vector.
   - For each element in the vector, the `std::multiplies` function object is used to multiply the element by 2. This effectively doubles each number in the vector.
   - The result replaces the original elements, so after this operation, `nums` will contain `{2, 4, 6, 8, 10}`.

3. Finding an Element with `std::find_if`:
   - The `std::find_if` algorithm searches the `nums` vector for the first element greater than 4.
   - It utilizes the `std::greater` function object for this comparison.
   - If such an element is found, its value is printed. In this case, the first number greater than 4 in the modified `nums` is 6.

4. Checking Even Numbers with `std::all_of`:
   - The `std::all_of` algorithm checks if a condition holds true for all elements in a range.
   - Here, it's used to verify if all numbers in the `nums` vector are even.
   - This is done by checking the modulus of each number with 2. If the result is 0 for all numbers, then all numbers are even.
   - Depending on the result, a corresponding message is printed.

5. Bitwise Operation with `std::bit_and`:
   - The `std::bit_and` function object performs a bitwise AND operation.
   - It's applied to the binary numbers `num` and `mask` defined earlier.
   - The result, `masked`, represents the number obtained after the AND operation on the two binary numbers.
   - This `masked` value is then printed.

Certainly! Let's break down `std::bind` and `std::placeholders::_1`:

### `std::bind`
`std::bind` is a utility in the C++ Standard Library that allows you to create a new callable object by binding one or more arguments to an existing function or functor. Essentially, it "binds" values to some of the parameters of a function, allowing you to create a new function with fewer parameters.

For example, consider a simple function that adds two numbers:
```cpp
int add(int a, int b) {
    return a + b;
}
```
Using `std::bind`, you can create a new function that always adds 5 to its argument:
```cpp
auto addFive = std::bind(add, 5, std::placeholders::_1);
```
Now, calling `addFive(3)` would return `8`.

### `std::placeholders::_1`
`std::placeholders::_1`, `_2`, `_3`, etc., are placeholders used with `std::bind` to represent the arguments that are not bound yet and will be provided later when the resulting bound function is called.

In the above example, `std::placeholders::_1` represents the first argument passed to the `addFive` function. When you call `addFive(3)`, the placeholder `_1` gets replaced with `3`.

### Together in Action
Consider a scenario where you have a function that checks if a number is divisible by another:
```cpp
bool isDivisible(int num, int divisor) {
    return num % divisor == 0;
}
```
You can use `std::bind` to create a new function that checks if a number is even:
```cpp
auto isEven = std::bind(isDivisible, std::placeholders::_1, 2);
```
Here, `std::placeholders::_1` will be replaced by the number you want to check, and `2` is the divisor. So, calling `isEven(4)` would return `true`.


## Creating Custom Function Objects
In addition to using predefined function objects, you can also create your own custom function objects. Custom function objects are typically implemented as classes that overload the `()` operator. Here's an example of a custom function object:
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

class Square {
public:
  int operator()(int x) const {
    return x * x;
  }
};

int main() {
  std::vector<int> nums = {1, 2, 3, 4, 5};

  Square square;
  std::transform(nums.begin(), nums.end(), nums.begin(), square);

  std::cout << "The squares of the elements in nums are: ";
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we define a custom function object called `Square` that computes the square of an integer. The `Square` class overloads the `()` operator, allowing objects of the class to be called like functions. We then use the `std::transform()` algorithm to apply the Square function object to each element in a `std::vector` of integers.

## Using Function Objects with Algorithms and Containers
Function objects can be used with a wide range of algorithms and containers in the STL. For example, the `std::sort()` algorithm can be customized with a comparison function object that specifies the order in which elements should be sorted. The `std::for_each()` algorithm can be used with a function object that performs some operation on each element in a range. Containers like `std::map` and std::set use function objects to order and compare their elements.

Here's an example of using a function object with the `std::sort()` algorithm:
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

class GreaterThan {
public:
  bool operator()(int a, int b) const {
    return a > b;
  }
};

int main() {
  std::vector<int> nums = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};

  GreaterThan greater_than;
  std::sort(nums.begin(), nums.end(), greater_than);

  std::cout << "The sorted elements of nums are: ";
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we use the `GreaterThan` function object to sort a `std::vector` of integers in descending order. The `GreaterThan` class overloads the `()` operator, allowing objects of the class to be called like functions. We then use the `std::sort()` algorithm to sort the vector using the `GreaterThan` function object to specify the sorting order.