
## STL Containers
STL containers are data structures used to store and manipulate collections of data. The STL provides several container classes, each with different characteristics and use cases.

### Overview of STL Container Classes
The STL provides several container classes, including:

* Sequence containers (vector, list, deque, forward_list): These containers provide a linear sequence of elements, allowing for efficient insertion and removal of elements at any position.

* Associative containers (set, multiset, map, multimap): These containers store elements in a sorted order and provide efficient access to elements based on their key.

* Unordered associative containers (unordered_set, unordered_multiset, unordered_map, unordered_multimap): These containers store elements in an unordered manner and provide efficient access to elements based on their key.

* Container adapters (stack, queue, priority_queue): These containers provide a specific interface for manipulating elements in a certain way, such as the LIFO behavior of a stack or the priority ordering of a priority queue.

## Sequence Containers
Sequence containers are containers that maintain the order of their elements. The STL provides several sequence container classes, including `std::vector`, `std::list`, `std::deque`, and `std::forward_list`.

### `std::vector`
`std::vector` is a dynamic array that can resize itself as elements are added or removed. It provides efficient random access to its elements and supports contiguous storage, making it a good choice for scenarios where elements need to be accessed frequently or in a random order. Here's an example of how to use `std::vector` in C++:
```cpp
#include <iostream>
#include <vector>

int main() {
  // Create a vector of integers
  std::vector<int> nums = {1, 2, 3, 4, 5};

  // Add an element to the end of the vector
  nums.push_back(6);

  // Insert an element at the beginning of the vector
  nums.insert(nums.begin(), 0);

  // Remove the last element from the vector
  nums.pop_back();

  // Print the elements of the vector
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::vector` of integers and initialize it with the values `{1, 2, 3, 4, 5}`. We then use the `std::vector::push_back()` member function to add an element with value 6 to the end of the vector, and the `std::vector::insert()` member function to insert an element with value 0 at the beginning of the vector. We use the `std::vector::pop_back()` member function to remove the last element from the vector. Finally, we use a for loop to print the elements of the vector to the console.

### `std::list`
`std::list` is a doubly-linked list that can efficiently insert or remove elements at any position. It does not support random access to its elements, so it is best suited for scenarios where elements need to be inserted or removed frequently, but not accessed randomly. Here's an example of how to use std::list in C++:
```cpp
#include <iostream>
#include <list>

int main() {
    // Create a list of strings
    std::list<std::string> names = {"Alice", "Bob", "Charlie"};

    // Insert a name at the beginning of
    // the list
    names.push_front("David");

    // Remove the second name from the list
    auto it = names.begin();
    std::advance(it, 1);
    names.erase(it);

    // Print the names in the list
    for (const std::string& name : names) {
    std::cout << name << " ";
    }
    std::cout << std::endl;

    return 0;
}
```
In this example, we create a `std::list` of strings and initialize it with the values `{"Alice", "Bob", "Charlie"}`. We use the `std::list::push_front()` member function to insert a name with value "David" at the beginning of the list. We use the `std::list::erase()` member function to remove the second name ("Bob") from the list, using an iterator to specify the position to be removed. Finally, we use a `for` loop to print the names in the list to the console.

### `std::deque`
`std::deque` (short for "double-ended queue") is a container that allows efficient insertion and removal of elements at the beginning and end of the container. It supports random access to its elements, making it a good choice for scenarios where elements need to be inserted or removed frequently at both ends of the container, or where random access is needed. Here's an example of how to use `std::deque` in C++:

```cpp
#include <iostream>
#include <deque>

int main() {
  // Create a deque of doubles
  std::deque<double> nums = {1.0, 2.0, 3.0, 4.0, 5.0};

  // Add an element to the beginning of the deque
  nums.push_front(0.0);

  // Remove the last element from the deque
  nums.pop_back();

  // Print the elements of the deque
  for (double num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::deque` of doubles and initialize it with the values `{1.0, 2.0, 3.0, 4.0, 5.0}`. We use the `std::deque::push_front()` member function to add an element with value 0.0 to the beginning of the deque, and the `std::deque::pop_back()` member function to remove the last element from the deque. Finally, we use a for loop to print the elements of the deque to the console.

### `std::forward_list`
`std::forward_list` is a singly-linked list that can efficiently insert or remove elements at the beginning or after any element. It does not support random access to its elements, so it is best suited for scenarios where elements need to be inserted or removed frequently at the beginning or after any element, but not accessed randomly. Here's an example of how to use `std::forward_list` in C++:
```cpp
#include <iostream>
#include <forward_list>

int main() {
    // Create a forward_list of integers
    std::forward_list<int> nums = {1, 2, 3, 4, 5};

    // Insert an element after the second element of the list
    auto it = nums.begin();
    std::advance(it, 1);
    nums.insert_after(it, 6);

    // Remove the first element from the list
    nums.pop_front();

    // Print the elements of the list
    for (int num :nums) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, we create a `std::forward_list` of integers and initialize it with the values `{1, 2, 3, 4, 5}`. We use an iterator to get the second element of the list, and the `std::forward_list::insert_after()` member function to insert an element with value 6 after the second element. We use the `std::forward_list::pop_front()` member function to remove the first element from the list. Finally, we use a `for` loop to print the elements of the list to the console.

## Associative Containers
Associative containers are containers that store elements in a sorted order based on their keys. The STL provides several associative container classes, including `std::set`, `std::multiset`, `std::map`, and `std::multimap`.

#### `std::set`
`std::set` is a container that stores unique elements in a sorted order based on their values. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where uniqueness and ordering are important. Here's an example of how to use `std::set` in C++:
```c++
#include <iostream>
#include <set>

int main() {
  // Create a set of integers
  std::set<int> nums = {3, 2, 1, 4, 5};

  // Insert an element into the set
  nums.insert(6);

  // Remove an element from the set
  nums.erase(4);

  // Print the elements of the set
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::forward_list` of integers and initialize it with the values `{1, 2, 3, 4, 5}`. We use an iterator to get the second element of the list, and the `std::forward_list::insert_after()` member function to insert an element with value 6 after the second element. We use the `std::forward_list::pop_front()` member function to remove the first element from the list. Finally, we use a `for` loop to print the elements of the list to the console.

### `std::multiset`
`std::multiset` is a container that stores non-unique elements in a sorted order based on their values. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where ordering is important and duplicate elements are allowed. Here's an example of how to use `std::multiset` in C++:
```cpp
#include <iostream>
#include <set>

int main() {
  // Create a multiset of integers
  std::multiset<int> nums = {3, 2, 1, 4, 5, 4};

  // Insert an element into the multiset
  nums.insert(6);

  // Remove an element from the multiset
  nums.erase(4);

  // Print the elements of the multiset
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::multiset` of integers and initialize it with the values `{3, 2, 1, 4, 5, 4}`. We use the `std::multiset::insert()` member function to add an element with value 6 to the multiset, and the `std::multiset::erase()` member function to remove the element with value 4 from the multiset. Finally, we use a for loop to print the elements of the multiset to the console.

### `std::map`
`std::map` is a container that stores key-value pairs in a sorted order based on their keys. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where key-value mappings are important and ordering by key is required. Here's an example of how to use `std::map` in C++:
```cpp
#include <iostream>
#include <map>

int main() {
  // Create a map of strings to integers
  std::map<std::string, int> scores = {{"Alice", 100}, {"Bob", 90}, {"Charlie", 80}};

  // Add a new key-value pair to the map
  scores.insert({"David", 70});

  // Update the value of an existing key in the map
  scores["Charlie"] = 85;

  // Remove a key-value pair from the map
  scores.erase("Bob");

  // Print the key-value pairs in the map
  for (const auto& [name, score] : scores) {
    std::cout << name << ": " << score << std::endl;
  }

  return 0;
}
```
In this example, we create a `std::map` that maps strings to integers and initialize it with the key-value pairs `{"Alice", 100}`, `{"Bob", 90}`, and `{"Charlie", 80}`. We use the `std::map::insert()` member function to add a new key-value pair with key "David" and value 70 to the map. We use the subscript operator `[]` to update the value associated with the key "Charlie" to 85. We use the `std::map::erase()` member function to remove the key-value pair with key "Bob" from the map. Finally, we use a `for` loop to print the key-value pairs in the map to the console.

### `std::multimap`
`std::multimap` is a container that stores multiple key-value pairs with the same key in a sorted order based on their keys. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where key-value mappings are important, ordering by key is required, and duplicate keys are allowed. Here's an example of how to use `std::multimap` in C++:
```cpp
#include <iostream>
#include <map>

int main() {
  // Create a multimap of strings to integers
  std::multimap<std::string, int> scores = {{"Alice", 100}, {"Bob", 90}, {"Charlie", 80}, {"Charlie", 85}};

  // Add a new key-value pair to the multimap
  scores.insert({"David", 70});

  // Remove all key-value pairs with key "Charlie" from the multimap
  scores.erase("Charlie");

  // Print the key-value pairs in the multimap
  for (const auto& [name, score] : scores) {
    std::cout << name << ": " << score << std::endl;
  }

  return 0;
}
```
In this example, we create a `std::multimap` that maps strings to integers and initialize it with the key-value pairs `{"Alice", 100}`, `{"Bob", 90}`, `{"Charlie", 80}`, and `{"Charlie", 85}`. We use the `std::multimap::insert()` member function to add a new key-value pair with key "David" and value 70 to the multimap. We use the `std::multimap::erase()` member function to remove all key-value pairs with key "Charlie" from the multimap. Finally, we use a for loop to print the key-value pairs in the multimap to the console.

## Unordered Associative Containers
### `std::unordered_set`
`std::unordered_set` is a container that stores unique elements in an unordered manner, based on their hash values. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where ordering is not important but uniqueness is required. Here's an example of how to use `std::unordered_set` in C++:
```cpp
#include <iostream>
#include <unordered_set>

int main() {
  // Create an unordered_set of integers
  std::unordered_set<int> nums = {3, 2, 1, 4, 5};

  // Insert an element into the unordered_set
  nums.insert(6);

  // Remove an element from the unordered_set
  nums.erase(4);

  // Print the elements of the unordered_set
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::unordered_set` of integers and initialize it with the values `{3, 2, 1, 4, 5}`. We use the `std::unordered_set::insert()` member function to add an element with value 6 to the unordered_set, and the `std::unordered_set::erase()` member function to remove the element with value 4 from the unordered_set. Finally, we use a for loop to print the elements of the unordered_set to the console.

### `std::unordered_multiset`
`std::unordered_multiset` is a container that stores non-unique elements in an unordered manner, based on their hash values. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where ordering is not important and duplicate elements are allowed. Here's an example of how to use `std::unordered_multiset` in C++:
```cpp
#include <iostream>
#include <unordered_set>

int main() {
  // Create an unordered_multiset of integers
  std::unordered_multiset<int> nums = {3, 2, 1, 4, 5, 4};

  // Insert an element into the unordered_multiset
  nums.insert(6);

  // Remove an element from the unordered_multiset
  nums.erase(4);

  // Print the elements of the unordered_multiset
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::unordered_multiset` of integers and initialize it with the values `{3, 2, 1, 4, 5, 4}`. We use the `std::unordered_multiset::insert()` member function to add an element with value 6 to the unordered_multiset, and the `std::unordered_multiset::erase()` member function to remove the elements with value 4 from the unordered_multiset. Finally, we use a for loop to print the elements of the unordered_multiset to the console.

### `std::unordered_map`
`std::unordered_map` is a container that stores key-value pairs in an unordered manner, based on their hash values. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where key-value mappings are important and ordering is not required. Here's an example of how to use `std::unordered_map` in C++:
```cpp
#include <iostream>
#include <unordered_map>

int main() {
  // Create an unordered_map of strings to integers
  std::unordered_map<std::string, int> scores = {{"Alice", 100}, {"Bob", 90}, {"Charlie", 80}};

  // Add a new key-value pair to the unordered_map
  scores.insert({"David", 70});

  // Update the value of an existing key in the unordered_map
  scores["Charlie"] = 85;

  // Remove a key-value pair from the unordered_map
  scores.erase("Bob");

  // Print the key-value pairs in the unordered_map
  for (const auto& [name, score] : scores) {
    std::cout << name << ": " << score << std::endl;
  }

  return 0;
}
```
In this example, we create a `std::unordered_map` that maps strings to integers and initialize it with the key-value pairs `{"Alice", 100}`, `{"Bob", 90}`, and `{"Charlie", 80}`. We use the `std::unordered_map::insert()` member function to add a new key-value pair with key "David" and value 70 to the unordered_map. We use the subscript operator `[]` to update the value associated with the key "Charlie" to 85. We use the `std::unordered_map::erase()` member function to remove the key-value pair with key "Bob" from the unordered_map. Finally, we use a for loop to print the key-value pairs in the unordered_map to the console.

### `std::unordered_multimap`
`std::unordered_multimap` is a container that stores multiple key-value pairs with the same key in an unordered manner, based on their hash values. It provides efficient search, insertion, and deletion of elements, making it a good choice for scenarios where key-value mappings are important, ordering is not required, and duplicate keys are allowed. Here's an example of how to use `std::unordered_multimap` in C++:
```cpp
#include <iostream>
#include <unordered_map>

int main() {
  // Create an unordered_multimap of strings to integers
  std::unordered_multimap<std::string, int> scores = {{"Alice", 100}, {"Bob", 90}, {"Charlie", 80}, {"Charlie", 85}};

  // Add a new key-value pair to the unordered_multimap
  scores.insert({"David", 70});

  // Remove all key-value pairs with key "Charlie" from the unordered_multimap
  scores.erase("Charlie");

  // Print the key-value pairs in the unordered_multimap
  for (const auto& [name, score] : scores) {
    std::cout << name << ": " << score << std::endl;
  }

  return 0;
}
```
In this example, we create a `std::unordered_multimap` that maps strings to integers and initialize it with the key-value pairs `{"Alice", 100}`, `{"Bob", 90}`, `{"Charlie", 80}`, and `{"Charlie", 85}`. We use the `std::unordered_multimap::insert()` member function to add a new key-value pair with key "David" and value 70 to the unordered_multimap. We use the `std::unordered_multimap::erase()` member function to remove all key-value pairs with key "Charlie" from the unordered_multimap. Finally, we use a for loop to print the key-value pairs in the unordered_multimap to the console.

## Container Adapters
### `std::stack`
`std::stack` is a container adapter that provides a LIFO (Last-In-First-Out) data structure. It uses a container (by default, std::deque) as its underlying storage, and provides a subset of the container's member functions as its interface. Here's an example of how to use `std::stack` in C++:
```cpp
#include <iostream>
#include <stack>

int main() {
  // Create a stack of integers
  std::stack<int> nums;

  // Push elements onto the stack
  nums.push(1);
  nums.push(2);
  nums.push(3);

  // Pop elements from the stack and print them
  while (!nums.empty()) {
    std::cout << nums.top() << " ";
    nums.pop();
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::stack` of integers and push the values 1, 2, and 3 onto the stack using the `std::stack::push()` member function. We use a while loop to pop elements from the stack using the `std::stack::top()` member function and print them to the console using `std::cout`. We use the `std::stack::empty()` member function to check if the stack is empty before popping an element.

### `std::queue`
`std::queue` is a container adapter that provides a FIFO (First-In-First-Out) data structure. It uses a container (by default, std::deque) as its underlying storage, and provides a subset of the container's member functions as its interface. Here's an example of how to use `std::queue` in C++:
```cpp
#include <iostream>
#include <queue>

int main() {
  // Create a queue of integers
  std::queue<int> nums;

  // Push elements into the queue
  nums.push(1);
  nums.push(2);
  nums.push(3);

  // Pop elements from the queue and print them
  while (!nums.empty()) {
    std::cout << nums.front() << " ";
    nums.pop();
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::queue` of integers and push the values 1, 2, and 3 into the queue using the `std::queue::push()` member function. We use a while loop to pop elements from the queue using the `std::queue::front()` member function and print them to the console using `std::cout`. We use the `std::queue::empty()` member function to check if the queue is empty before popping an element.

### `std::priority_queue`
`std::priority_queue` is a container adapter that provides a priority queue data structure. It uses a container (by default, std::vector) as its underlying storage, and maintains a sorted order of elements based on a comparison function. Here's an example of how to use `std::priority_queue` in C++:
```cpp
#include <iostream>
#include <queue>

int main() {
    // Create a priority queue of integers
    std::priority_queue<int> nums;

    // Push elements into the priority queue
    nums.push(3);
    nums.push(1);
    nums.push(2);

    // Pop elements from the priority queue and print them
    while (!nums.empty())
    {
        std::cout << nums.top() << " ";
        nums.pop();
    }
    std::cout << std::endl;

    return 0;
}
```
In this example, we create a `std::priority_queue` of integers and push the values 3, 1, and 2 into the priority queue using the `std::priority_queue::push()` member function. The priority queue automatically sorts the elements in descending order (highest value first) because we did not provide a comparison function. We use a `while` loop to pop elements from the priority queue using the `std::priority_queue::top()` member function and print them to the console using `std::cout`. We use the `std::priority_queue::empty()` member function to check if the priority queue is empty before popping an element.

## Choosing the Appropriate Container
When choosing a container to use in a particular scenario, it's important to consider the requirements of the application and the characteristics of each container. Here are some guidelines for choosing the appropriate container:

- Use `std::vector` when:
  - You need a dynamic array with contiguous memory.
  - You frequently need to add or remove elements from the back of the container.
  - You don't need to insert or remove elements from the middle of the container frequently.
  - You don't need to search the container frequently.
- Use `std::list` when:
  - You need a doubly-linked list with constant-time insertion and removal of elements anywhere in the container.
  - You don't need to access elements by their index frequently.
- Use `std::deque` when:
  - You need a double-ended queue with constant-time insertion and removal of elements at the beginning and end of the container.
  - You don't need to insert or remove elements from the middle of the container frequently.
- Use `std::set` or `std::map` when:
  - You need a container that stores unique elements in sorted order.
  - You need to search the container frequently.
  - You don't need to access elements by their index.
  - You don't need to insert or remove elements from the middle of the container frequently.
- Use `std::unordered_set` or `std::unordered_map` when:
  - You need a container that stores unique elements in unordered manner, based on their hash values.
  - You need to search, insert, and remove elements efficiently.
  - You don't need to access elements by their index.
  - You don't need to insert or remove elements from the middle of the container frequently.
- Use `std::multiset` or `std::multimap` when:
  - You need a container that stores non-unique elements in sorted order.
  - You need to search the container frequently.
  - You don't need to access elements by their index.
  - You don't need to insert or remove elements from the middle of the container frequently.
- Use `std::unordered_multiset` or `std::unordered_multimap` when:
  - You need a container that stores non-unique elements in an unordered manner, based on their hash values.
  - You need to search, insert, and remove elements efficiently.
  - You don't need to access elements by their index.
  - You don't need to insert or remove elements from the middle of the container frequently.
- Use `std::stack`, `std::queue`, or `std::priority_queue` when:
  - You need a specific data structure (LIFO, FIFO, or priority queue, respectively).
  - You don't need to access elements by their index.
  - You don't need to search the container frequently.
  - You don't need to insert or remove elements from the middle of the container frequently.

It's important to note that these guidelines are not strict rules, and there may be cases where a container that deviates from these guidelines is more appropriate for a particular scenario. It's also possible to combine multiple containers to achieve a desired functionality.