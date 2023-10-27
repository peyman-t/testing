## STL Allocators
STL allocators provide a mechanism for controlling the memory allocation and deallocation behavior of containers and other components in the STL. In this section, we'll cover the basic concepts of STL allocators, including their role in the STL, understanding memory allocation and deallocation in STL containers, and creating custom allocators.

### Overview of STL Allocators
STL allocators provide a mechanism for controlling the memory allocation and deallocation behavior of containers and other components in the STL. They allow you to specify a custom memory allocation strategy for a container, and are used extensively in the STL to provide efficient and flexible memory management.

STL allocators are typically implemented as classes that provide the following functions:

* `allocate()`: Allocates a block of memory of a specified size.
* `deallocate()`: Deallocates a block of memory that was previously allocated using the same allocator.
* `construct()`: Constructs an object at a specified location in memory.
* `destroy()`: Destructs an object at a specified location in memory.

## Understanding Memory Allocation and Deallocation in STL Containers
STL containers use allocators to manage their memory allocation and deallocation behavior. When you create a container object, it uses the default allocator for the container's element type. For example, a `std::vector<int>` object uses the default allocator for `int` elements.

Here's an example of creating a `std::vector<int>` object and pushing elements onto it:
```cpp
#include <iostream>
#include <vector>

int main() {
  std::vector<int> nums;

  nums.push_back(1);
  nums.push_back(2);
  nums.push_back(3);

  std::cout << "The elements of nums are: ";
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we create a `std::vector<int>` object and push three elements onto it. The `std::vector<int>` object uses the default allocator for int elements to allocate and deallocate memory for the elements.

## Creating Custom Allocators
In addition to using the default allocator, you can also create your own custom allocator to control the memory allocation and deallocation behavior of a container. Custom allocators are typically implemented as classes that provide the `allocate()`, `deallocate()`, `construct()`, and `destroy()` functions. Here's an example of creating a custom allocator:
```cpp
#include <iostream>
#include <vector>

template<typename T>
class MyAllocator {
public:
  using value_type = T;

  T* allocate(std::size_t n) {
    std::cout << "Allocating " << n << " elements" << std::endl;
    return static_cast<T*>(::operator new(n * sizeof(T)));
  }

  void deallocate(T* p, std::size_t n) {
    std::cout << "Deallocating " << n << " elements" << std::endl;
    ::operator delete(p);
  }

  template<typename U, typename... Args>
  void construct(U* p, Args&&... args) {
    std::cout << "Constructing element" << std::endl;
    new (p) U(std::forward<Args>(args)...);
  }

  template<typename U>
  void destroy(U* p) {
    std::cout << "Destroying element" << std::endl;
    p->~U();
  }
};

int main() {
  std::vector<int, MyAllocator<int>> nums;

  nums.push_back(1);
  nums.push_back(2);
  nums.push_back(3);

  std::cout << "The elements of nums are: ";
  for (int num : nums) {
    std::cout << num << " ";
  }
  std::cout << std::endl;

  return 0;
}
```
In this example, we define a custom allocator called `MyAllocator` that provides the `allocate()`, `deallocate()`, `construct()`, and `destroy()` functions. The `allocate()` function allocates a block of memory of a specified size, and the `deallocate()` function deallocates a block of memory that was previously allocated using the same allocator. The `construct()` and `destroy()` functions are used to construct and destruct objects at specific locations in memory.

We then create a `std::vector<int>` object using our custom allocator, and push three elements onto it. The `MyAllocator<int>` allocator is used to allocate and deallocate memory for the elements in the vector. Finally, we print the elements of the vector to the console.

Output:
```cpp
Allocating 1 elements
Constructing element
Allocating 2 elements
Constructing element
Constructing element
The elements of nums are: 1 2 3 
Destroying element
Destroying element
Deallocating 3 elements
```
In the output, we can see that the custom allocator is used to allocate and deallocate memory for the vector elements, and also to construct and destruct the elements.

