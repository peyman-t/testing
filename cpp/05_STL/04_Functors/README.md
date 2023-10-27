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
                              std::bind(std::modulus<int>(), std::placeholders::_1, 2) == 0);
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
In this example, we use predefined function objects to perform arithmetic, relational, logical, and bitwise operations on a `std::vector` of integers. The `std::multiplies<int>` function object is used to multiply each element in the vector by 2. The `std::greater<int>` function object is used to find the first element in the vector that is greater than 4. The `std::modulus<int>` function object is used with the `std::bind()` function to determine if all elements in the vector are even. The `std::bit_and<int>` function object is used to mask off the lower 4 bits of an integer.

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