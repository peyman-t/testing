
## Type Traits (C++11 onwards)
Type traits are a set of templates and classes introduced in C++11 that allow for introspecting and modifying types at compile-time.

### Introduction to Type Traits
Type traits are templates and classes that provide information about types at compile-time. They are used to query the properties of types, such as whether they are pointers or arrays, whether they are const or volatile, and whether they are arithmetic or integral types.

### Using Type Traits to Introspect and Modify Types at Compile-Time
Here's an example of using the `std::is_pointer` type trait to check if a type is a pointer:
```cpp
#include <iostream>
#include <type_traits>
using namespace std;

int main() {
    cout << boolalpha;
    cout << "Is int* a pointer? " << is_pointer<int*>::value << endl;
    cout << "Is char* a pointer? " << is_pointer<char*>::value << endl;
    cout << "Is double a pointer? " << is_pointer<double>::value << endl;

    return 0;
}
```
In this example, we have used the `std::is_pointer` type trait to check if a type is a pointer. The `is_pointer` template takes a type as its template argument, and has a boolean `value` member that indicates whether the type is a pointer or not.

The `main` function uses the `is_pointer` type trait to check if `int*`, `char*`, and `double` are pointers. The boolean value of each check is printed to the console.

Here's an example of using the `std::enable_if` type trait to enable a function only if a condition is true:
```cpp
#include <iostream>
#include <type_traits>
using namespace std;

// Function that is enabled only for integral types
template <typename T>
typename enable_if<is_integral<T>::value, T>::type
my_function(T x) {
    return x * 2;
}

int main() {
    cout << my_function(10) << endl; // Output: 20
    // cout << my_function("hello") << endl; // Compile error

    return 0;
}
```
In this example, we have used the `std::enable_if` type trait to enable a function only for integral types. The `enable_if` template takes a boolean condition as its first template argument, and the type to be enabled as its second template argument. If the condition is true, the type is enabled; otherwise, the function is not defined.

The `my_function` function is defined for integral types only using the `enable_if` type trait. The function multiplies its argument by 2 and returns the result.

The `main` function calls the `my_function` function with an integer argument, and prints the result to the console. It also tries to call the function with a string argument, but this results in a compile error since the function is not defined for non-integral types.

### Examples of Type Traits in C++ Code
Here are a few more examples of type traits:
```cpp
#include <iostream>
#include <type_traits>
using namespace std;

int main() {
    // Checking if a type is an array
    cout << boolalpha;
    cout << "Is int[] an array? " << is_array<int[]>::value << endl;
    cout << "Is int* an array? " << is_array<int*>::value << endl;

    // Checking if a type is const-qualified
    cout << "Is const int a const-qualified type? " << is_const<const int>::value << endl
    cout << "Is int a const-qualified type? " << is_const<int>::value << endl;

    // Checking if a type is a pointer to a member
    class MyClass {
    public:
        int member_variable;
    };
    typedef int MyClass::*MemberPtr;
    cout << "Is int MyClass::* a pointer-to-member type? " << is_member_pointer<MemberPtr>::value << endl;
    cout << "Is int* a pointer-to-member type? " << is_member_pointer<int*>::value << endl;

    return 0;
}
```
In this example, we have used the `std::is_array`, `std::is_const`, and `std::is_member_pointer` type traits to check various properties of types.

The `is_array` type trait is used to check if a type is an array. The `is_const` type trait is used to check if a type is const-qualified. The `is_member_pointer` type trait is used to check if a type is a pointer to a member of a class.

The `main` function uses the type traits to check the properties of various types and prints the boolean results to the console.