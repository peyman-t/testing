## Passing Structs to Functions
Structs can be passed to functions just like any other data type. There are three ways to pass a struct to a function: pass-by-value, pass-by-reference, and pass-by-pointer.

### Pass-by-value
When a struct is passed by value, a copy of the entire struct is made and passed to the function. This can be inefficient for large structs, as the entire struct needs to be copied each time it is passed to a function. However, it is useful for small structs that need to be modified within a function without affecting the original struct.

Here's an example of passing a struct by value:
```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

void printPoint(Point p) {
    std::cout << "(" << p.x << ", " << p.y << ")" << std::endl;
}

int main() {
    Point p = {3, 4};
    printPoint(p);
    return 0;
}
```
In this example, we define a struct named `Point` with two member variables: `x` and `y`. We also define a function named `printPoint` that takes a `Point` struct as a parameter and displays its `x` and `y` member variables using `std::cout`.

In the `main()` function, we create a `Point` object named `p`, set its `x` and `y` member variables to 3 and 4, respectively, and pass it to the `printPoint` function by value. The `printPoint` function receives a copy of `p` and displays its `x` and `y` member variables.

### Pass-by-reference
When a struct is passed by reference, a reference to the original struct is passed to the function. This is more efficient than pass-by-value for large structs, as the entire struct is not copied each time it is passed to a function. Additionally, any modifications made to the struct within the function will affect the original struct.

Here's an example of passing a struct by reference:
```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

void incrementX(Point& p) {
    p.x++;
}

int main() {
    Point p = {3, 4};
    incrementX(p);
    std::cout << "x: " << p.x << ", y: " << p.y << std::endl;
    return 0;
}
```
In this example, we define a function named `incrementX` that takes a `Point` struct by reference and increments its `x` member variable.

In the `main()` function, we create a `Point` object named `p`, set its `x` and `y` member variables to 3 and 4, respectively, and pass it to the `incrementX` function by reference. The `incrementX` function modifies the `x` member variable of `p`, which affects the original `p` object.

### Pass-by-pointer
When a struct is passed by pointer, a pointer to the original struct is passed to the function. This is similar to pass-by-reference, but requires the use of the pointer dereference operator `*` within the function to access the member variables of the struct.

Here's an example of passing a struct by pointer:
```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

void decrementY(Point* p) {
    (*p).y--;
}

int main() {
    Point p = {3, 4};
    decrementY(&p);
    std::cout << "x: " << p.x << ", y: " << p.y << std::endl;
    return 0;
}
```
In this example, we define a function named `decrementY` that takes a pointer to a `Point` struct and decrements its `y` member variable using the pointer dereference operator `*`.

In the `main()` function, we create a `Point` object named `p`, set its `x` and `y` member variables to 3 and 4, respectively, and pass a pointer to `p` to the `decrementY` function. The `decrementY` function uses the pointer dereference operator `*` to access the `y` member variable of `p` and decrement it. The original `p` object is modified by the function.

Each of the three ways of passing a struct to a function in C++ has its own advantages and disadvantages.

* Pass-by-value:
    * Advantages:

        * The function receives a copy of the struct, which prevents the original struct from being modified by the function.
        * It can be useful for small structs that do not need to be modified by the function.
    * Disadvantages:

        * It can be inefficient for large structs, as the entire struct needs to be copied each time it is passed to a function.
* Pass-by-reference:
    * Advantages:

        * It is more efficient than pass-by-value for large structs, as only a reference to the original struct is passed to the function.
        * Any modifications made to the struct within the function will affect the original struct.
    * Disadvantages:

        * It can be dangerous if the function modifies the struct in unexpected ways, as this can cause unintended side effects in the rest of the program.
* Pass-by-pointer:
    * Advantages:

        * It is similar to pass-by-reference, but requires the use of a pointer.
        * Any modifications made to the struct within the function will affect the original struct.
    * Disadvantages:

        * It can be dangerous if the pointer is not properly initialized or if the function modifies the struct in unexpected ways.
        * It can be more difficult to read and understand than pass-by-value or pass-by-reference.

> **Note**
>
> In general, pass-by-reference or pass-by-pointer are often preferred for large structs, as they are more efficient and allow the function to modify the original struct. However, pass-by-value can be useful for small structs that do not need to be modified by the function.

## Returning Structs from Functions
Structs can be returned from functions just like any other data type. There are three ways to return a struct from a function: return-by-value, return-by-reference, and return-by-pointer.

### Return-by-value
When a struct is returned by value, a copy of the entire struct is made and returned by the function. This can be inefficient for large structs, as the entire struct needs to be copied each time it is returned from a function. However, it is useful for small structs that need to be returned from a function without affecting the original struct.

Here's an example of returning a struct by value:
```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

Point createPoint(int x, int y) {
    Point p = {x, y};
    return p;
}

int main() {
    Point p = createPoint(3, 4);
    std::cout << "(" << p.x << ", " << p.y << ")" << std::endl;
    return 0;
}
```
In this example, we define a struct named `Point` with two member variables: `x` and `y`. We also define a function named `createPoint` that takes two `int` parameters, creates a `Point` struct with those parameters, and returns the `Point` struct by value.

In the `main()` function, we call the `createPoint` function with `x` and `y` values of 3 and 4, respectively, and assign the returned `Point` struct to a `Point` variable named `p`. We then display the `x` and `y` member variables of `p` using `std::cout`.

### Return-by-reference
When a struct is returned by reference, a reference to the original struct is returned by the function. This is more efficient than return-by-value for large structs, as the entire struct is not copied each time it is returned from a function. Additionally, any modifications made to the struct within the function will affect the original struct.

Here's an example of returning a struct by reference:
```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

Point& getOrigin() {
    static Point origin = {0, 0};
    return origin;
}

int main() {
    Point& originRef = getOrigin();
    std::cout << "(" << originRef.x << ", " << originRef.y << ")" << std::endl;
    return 0;
}
```
In this example, we define a function named `getOrigin` that returns a reference to a `Point` struct representing the origin `(0, 0)`. We use the `static` keyword to ensure that the `origin` struct persists between function calls.

In the `main()` function, we call the `getOrigin` function and assign the returned reference to a `Point` reference variable named `originRef`. We then display the `x` and `y` member variables of `originRef` using `std::cout`.

### Return-by-pointer
When a struct is returned by pointer, a pointer to the original struct is returned by the function. This is similar to return-by-reference, but requires the use of the pointer dereference operator `*` to access the member variables of the struct.

Here's an example of returning a struct by pointer:
```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

Point* createPoint(int x, int y) {
    Point* p = new Point;
    p->x = x;
    p->y = y;
    return p;
}

int main() {
    Point* p = createPoint(3, 4);
    std::cout << "(" << p->x << ", " << p->y << ")" << std::endl;
    delete p;
    return 0;
}
```
In this example, we define a function named `createPoint` that takes two `int` parameters, creates a `Point` struct using dynamic memory allocation with `new`, sets the `x` and `y` member variables of the `Point` struct using the arrow operator `->`, and returns a pointer to the `Point` struct.

In the `main()` function, we call the `createPoint` function with `x` and `y` values of `3` and `4`, respectively, and assign the returned pointer to a `Point` pointer variable named `p`. We then display the `x` and `y` member variables of the `Point` struct using the arrow operator `->`, and delete the `Point` struct using `delete` to free the dynamically allocated memory.

> **Note**
>
> Return-by-value is useful for small structs that do not require modification, but can be inefficient for large structs, as the entire struct is copied each time it is returned from a function.
>  
> Return-by-reference is more efficient for large structs, as a reference to the original struct is returned instead of a copy, but can be dangerous if the function modifies the struct in unexpected ways.
>  
> Return-by-pointer is similar to return-by-reference, but requires the use of the pointer dereference operator to access the member variables of the struct. It is also useful for dynamic memory allocation. Overall, each method has its own advantages and disadvantages, and the choice of which one to use depends on the specific needs of the program.