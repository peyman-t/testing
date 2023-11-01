## STL Algorithms
The STL provides a rich set of algorithms that operate on containers using iterators. These algorithms can be used with any container that provides the appropriate iterators. In this section, we'll cover the basic categories of algorithms in the STL, including non-modifying sequence algorithms, modifying sequence algorithms, sorting and related operations, and numeric operations.

### Overview of STL Algorithms
STL algorithms are functions that operate on ranges and can be used to perform a variety of operations on containers. Algorithms can be divided into several categories based on their functionality, including:

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

Here's an example demonstrating the above algorithms:
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to print each element
void printElement(int n) {
    std::cout << n << " ";
}

int main() {
    std::vector<int> vec1 = {1, 2, 3, 4, 5, 3, 7};
    std::vector<int> vec2 = {1, 2, 3, 4, 6, 3, 7};
    std::vector<int> subVec = {4, 5, 3};

    // Applies the printElement function to each element in vec1
    std::for_each(vec1.begin(), vec1.end(), printElement);
    std::cout << std::endl;

    // Counts the number of occurrences of '3' in vec1
    int countThree = std::count(vec1.begin(), vec1.end(), 3);
    std::cout << "Number of occurrences of 3: " << countThree << std::endl;

    // Finds the first occurrence of '5' in vec1
    std::vector<int>::iterator itFind = std::find(vec1.begin(), vec1.end(), 5);
    if (itFind != vec1.end()) {
        std::cout << "Found 5 at position: " << (itFind - vec1.begin()) << std::endl;
    }

    // Searches for the sequence in subVec within vec1
    std::vector<int>::iterator itSearch = std::search(vec1.begin(), vec1.end(), subVec.begin(), subVec.end());
    if (itSearch != vec1.end()) {
        std::cout << "Found sub-sequence starting at position: " << (itSearch - vec1.begin()) << std::endl;
    }

    // Compares vec1 and vec2 for equality
    bool areEqual = std::equal(vec1.begin(), vec1.end(), vec2.begin());
    std::cout << "vec1 and vec2 are " << (areEqual ? "equal." : "not equal.") << std::endl;

    // Finds the first mismatch between vec1 and vec2
    std::pair<std::vector<int>::iterator, std::vector<int>::iterator> itMismatch = std::mismatch(vec1.begin(), vec1.end(), vec2.begin());
    if (itMismatch.first != vec1.end()) {
        std::cout << "First mismatch found at position: " << (itMismatch.first - vec1.begin()) << ". "
                  << "vec1 has " << *(itMismatch.first) << ", while vec2 has " << *(itMismatch.second) << "." << std::endl;
    }

    return 0;
}
```
The code starts by including necessary headers for input-output operations, the vector container, and algorithm functions. A function named `printElement` is defined which simply prints an integer followed by a space. 

Three vectors, `vec1`, `vec2`, and `subVec`, are initialized with integer values. The `for_each` algorithm, combined with the `printElement` function, prints each element of `vec1`. 

The `count` algorithm determines how many times the number '3' appears in `vec1`. 

The `find` algorithm locates the first occurrence of the number '5' in `vec1`. 

The `search` algorithm looks for the sequence present in `subVec` within `vec1` and indicates its starting position. 

The `equal` algorithm checks if `vec1` and `vec2` are identical. 

Finally, the `mismatch` algorithm identifies the first position where `vec1` and `vec2` differ and displays the differing values from both vectors.

## Modifying Sequence Algorithms
Modifying sequence algorithms modify the container by changing the order, adding or removing elements, or replacing elements in a sequence. The following are some of the most common modifying sequence algorithms in the STL:

* `copy()`: Copies elements from one range to another.

* `move()`: Moves elements from one range to another.

* `swap()`: Swaps the values of two elements.

* `fill()`: Fills a range with a given value.

* `replace()`: Replaces all occurrences of a value in a range with another value.

* `remove()`: Removes all occurrences of a value from a range.

Here's an example of using the above algorithms:
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    // Initializes two vectors with integer values
    std::vector<int> vec1 = {1, 2, 3, 4, 5};
    std::vector<int> vec2(5);  // A vector of size 5, uninitialized

    // Copies elements from vec1 to vec2
    std::copy(vec1.begin(), vec1.end(), vec2.begin());

    // Moves elements from vec2 back to vec1
    std::move(vec2.begin(), vec2.end(), vec1.begin());

    // Swaps the first element of vec1 with the second
    std::swap(vec1[0], vec1[1]);

    // Fills vec2 with the value 10
    std::fill(vec2.begin(), vec2.end(), 10);

    // Replaces all occurrences of '2' in vec1 with '20'
    std::replace(vec1.begin(), vec1.end(), 2, 20);

    // Removes all occurrences of '3' from vec1
    vec1.erase(std::remove(vec1.begin(), vec1.end(), 3), vec1.end());

    // Prints the elements of vec1
    for (int val : vec1) {
        std::cout << val << " ";
    }

    return 0;
}
```
In this code:
- Two vectors, `vec1` and `vec2`, are initialized.
- The `copy` algorithm copies elements from `vec1` to `vec2`.
- The `move` algorithm transfers the elements back from `vec2` to `vec1`.
- The `swap` algorithm exchanges the values of the first two elements of `vec1`.
- The `fill` algorithm sets all elements of `vec2` to the value `10`.
- The `replace` algorithm changes all occurrences of the value `2` in `vec1` to `20`.
- The `remove` algorithm deletes all occurrences of the value `3` from `vec1`, and the `erase` method then erases the "removed" elements from the vector.
- Finally, the modified `vec1` is printed to the console.

Note that the `std::remove` algorithm doesn't actually remove elements from a container. Instead, it reorders the elements so that the elements to be "removed" are moved to the end, and then returns an iterator pointing to the first of these elements. To actually remove these elements from a container like `std::vector`, you'd typically use the `erase` method in combination with `std::remove`.

## Numeric Operations
Numeric operations perform arithmetic operations on the elements of a container, such as computing the sum, product, or inner product of a sequence. The following are some of the most common numeric operations in the STL:

* `accumulate()`: Computes the sum of the elements in a range.

* `inner_product()`: Computes the inner product of two ranges.

* `partial_sum()`: Computes the partial sum of a range.

* `adjacent_difference()`: Computes the differences between adjacent elements in a range.

Here's an example demonstrating the above algorithms:
```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    // Initializes two vectors with integer values
    std::vector<int> vec1 = {1, 2, 3, 4, 5};
    std::vector<int> vec2 = {5, 4, 3, 2, 1};
    std::vector<int> result(vec1.size());

    // Computes the sum of all elements in vec1
    int sum = std::accumulate(vec1.begin(), vec1.end(), 0);
    std::cout << "Sum of vec1: " << sum << std::endl;

    // Computes the inner product of vec1 and vec2
    int product = std::inner_product(vec1.begin(), vec1.end(), vec2.begin(), 0);
    std::cout << "Inner product of vec1 and vec2: " << product << std::endl;

    // Computes the partial sum of vec1 and stores it in result
    std::partial_sum(vec1.begin(), vec1.end(), result.begin());
    std::cout << "Partial sum of vec1: ";
    for (int val : result) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    // Computes the differences between adjacent elements in vec1 and stores it in result
    std::adjacent_difference(vec1.begin(), vec1.end(), result.begin());
    std::cout << "Adjacent differences of vec1: ";
    for (int val : result) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    return 0;
}
```
In this code:

- Two vectors, `vec1` and `vec2`, are initialized with integer values.
- The `accumulate` algorithm calculates the sum of all elements in `vec1`.
- The `inner_product` algorithm calculates the dot product of `vec1` and `vec2`.
- The `partial_sum` algorithm computes the cumulative sum of elements in `vec1` and stores the result in the `result` vector.
- The `adjacent_difference` algorithm calculates the difference between each element and its preceding element in `vec1` and stores the result in the `result` vector.

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

