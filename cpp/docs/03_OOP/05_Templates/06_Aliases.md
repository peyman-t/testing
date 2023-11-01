
## Template Type Aliases (C++11 onwards) and typedefs
Template type aliases and typedefs are features introduced in C++11 that allow for defining aliases for complex types and templates.

### Definition and Syntax of Template Type Aliases and typedefs
Here's an example of using a template type alias to define a complex type:
```cpp
#include <iostream>
#include <vector>
using namespace std;

// Template type alias to define a vector of integers
template <typename T>
using IntVector = vector<T>;

int main() {
    IntVector<int> v = {1, 2, 3, 4, 5};
    for (const auto& i : v) {
        cout << i << " ";
    }
    cout << endl;

    return 0;
}
```
In this example, we have defined a template type alias `IntVector` that defines a vector of a specified data type. The template type alias is defined using the `using` keyword, and is followed by the template parameter and the underlying type.

The `main` function creates a vector of integers using the `IntVector` template type alias, and initializes it with five integer values. The values are then printed to the console.

In the above code, the `auto` keyword is used in the range-based for loop to automatically deduce the type of the elements in the `IntVector<int>` container.

Here's a breakdown of its usage:

1. `const auto& i` - The `auto` keyword is used to automatically deduce the type of each element in the `IntVector<int>`. By using `auto`, we don't need to explicitly specify the type of the elements.

2. `const` - The `const` qualifier is used to indicate that the loop variable `i` is read-only and cannot be modified within the loop.

By using `auto` in the range-based for loop, the code becomes more concise and flexible. It adapts to the specific type contained in the `IntVector<int>` without requiring manual specification. This is particularly useful when dealing with complex or generic types, as it eliminates the need to update the code if the container's type changes.

Here's an example of using a `typedef` to define a complex type:
```cpp
#include <iostream>
using namespace std;

// Typedef to define an array of integers
typedef int IntArray[];

int main() {
    IntArray v = {1, 2, 3, 4, 5};
    for (const auto& i : v) {
        cout << i << " ";
    }
    cout << endl;

    return 0;
}
```
In this example, we have defined a `typedef` called `IntArray` which represents an array of integers. The `IntArray` is then initialized with the values `{1, 2, 3, 4, 5}`.

The range-based for loop uses `auto` to deduce the type of each element in the `IntArray`. The loop iterates over each element `i` and prints it to the console.

Note that when using an array in this way, the size of the array must be known at compile-time.