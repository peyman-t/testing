## STL Algorithms
The STL provides a rich set of algorithms that operate on containers using iterators. These algorithms can be used with any container that provides the appropriate iterators. In this section, we'll cover the basic categories of algorithms in the STL, including non-modifying sequence algorithms, modifying sequence algorithms, sorting and related operations, and numeric operations.

### Overview of STL Algorithms
STL algorithms are functions that operate on iterators and can be used to perform a variety of operations on containers. Algorithms can be divided into several categories based on their functionality, including:

* Non-modifying sequence algorithms: These algorithms do not modify the container and are used to search, count, or compare elements in a sequence.

* Modifying sequence algorithms: These algorithms modify the container by changing the order, adding or removing elements, or replacing elements in a sequence.

* Sorting and related operations: These algorithms are used to sort the elements of a container or perform related operations, such as finding the first element that is not less than a given value.

* Numeric operations: These algorithms perform arithmetic operations on the elements of a container, such as computing the sum, product, or inner product of a sequence.

In the following subsections, we'll cover each category of algorithm in more detail.

## Non-modifying Sequence Algorithms
Non-modifying sequence algorithms do not modify the container and are used to search, count, or compare elements in a sequence. The following are some of the most common non-modifying sequence algorithms in the STL:

* `for_each()`: Applies a function to each element in a range.

* `count()`: Counts the number of elements in a range that are equal to a given value.

* `find()`: Finds the first occurrence of a value in a range.

* `search()`: Searches for a sequence of elements in a range.

* `equal()`: Compares two ranges for equality.

* `mismatch()`: Finds the first position where two ranges differ.

Here's an example of using the `std::count()` algorithm with a `std::vector`:
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> nums = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

  int count = std::count(nums.begin(), nums.end(), 5);

  std::cout << "The number of occurrences of 5 in nums is " << count << std::endl;

  return 0;
}
```
In this example, we use the `std::count()` algorithm to count the number of occurrences of the value 5 in a `std::vector` of integers. The first two arguments to `std::count()` are iterators that specify the range of elements to search, and the third argument is the value to count. The return value of `std::count()` is the number of elements that are equal to the given value.

## Modifying Sequence Algorithms
Modifying sequence algorithms modify the container by changing the order, adding or removing elements, or replacing elements in a sequence. The following are some of the most common modifying sequence algorithms in the STL:

* `copy()`: Copies elements from one range to another.

* `move()`: Moves elements from one range to another.

* `swap()`: Swaps the values of two elements.

* `fill()`: Fills a range with a given value.

* `replace()`: Replaces all occurrences of a value in a range with another value.

* `remove()`: Removes all occurrences of a value from a range.

Here's an example of using the `std::sort()` algorithm with a `std::vector`:
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> nums = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};

  std::sort(nums.begin(), nums.end());

  std::cout << "The sorted elements of nums are: ";
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
n this example, we use the `std::sort()` algorithm to sort a `std::vector` of integers in ascending order. The first two arguments to `std::sort()` are iterators that specify the range of elements to sort. The third argument is an optional comparison function that is used to compare elements in the range. If no comparison function is specified, the default comparison function (`std::less`) is used.

## Numeric Operations
Numeric operations perform arithmetic operations on the elements of a container, such as computing the sum, product, or inner product of a sequence. The following are some of the most common numeric operations in the STL:

* `accumulate()`: Computes the sum of the elements in a range.

* `inner_product()`: Computes the inner product of two ranges.

* `partial_sum()`: Computes the partial sum of a range.

* `adjacent_difference()`: Computes the differences between adjacent elements in a range.

Here's an example of using the `std::accumulate()` algorithm with a `std::vector`:
```cpp
#include <iostream>
#include <numeric>
#include <vector>

int main() {
  std::vector<int> nums = {1, 2, 3, 4, 5};

  int sum = std::accumulate(nums.begin(), nums.end(), 0);

  std::cout << "The sum of the elements in nums is " << sum << std::endl;

  return 0;
}
```
In this example, we use the `std::accumulate()` algorithm to compute the sum of the elements in a `std::vector` of integers. The first two arguments to `std::accumulate()` are iterators that specify the range of elements to sum, and the third argument is an initial value that is used to start the accumulation process. The return value of `std::accumulate()` is the result of the accumulation process.

## Customizing Algorithms with Predicates
Many algorithms in the STL can be customized with predicates, which are functions or function objects that take one or more arguments and return a boolean value. Predicates are used to specify a condition that an algorithm should use to perform its operation. For example, the `std::sort()` algorithm can be customized with a comparison function that specifies the order in which elements should be sorted.

Here's an example of using the `std::sort()` algorithm with a custom comparison function:
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

bool compare(int a, int b) {
  return a > b;
}

int main() {
  std::vector<int> nums = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};

  std::sort(nums.begin(), nums.end(), compare);

  std::cout << "The sorted elements of nums are: ";
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we use the `std::sort()` algorithm to sort a `std::vector` of integers in descending order by providing a custom comparison function. The `compare()` function takes two integer arguments and returns true if the first argument is greater than the second argument, and false otherwise.

