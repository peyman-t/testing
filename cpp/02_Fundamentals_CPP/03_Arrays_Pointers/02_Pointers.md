
## Pointers
A pointer is a powerful feature in C++ that allows for direct access and manipulation of memory. In essence, a pointer is a variable that holds the memory address of another variable. By using pointers, we can access and modify the data stored in that memory address. Pointers are useful for a variety of tasks such as accessing individual elements in an array, iterating over an array, and dynamically allocating memory at runtime. Additionally, pointers are frequently used when passing data to functions, allowing for the efficient and flexible transfer of data between different parts of a program. While pointers are a powerful tool, they can also be a source of errors such as memory leaks and null pointers. Therefore, it is important to use pointers carefully and correctly in order to avoid these issues and maximize the benefits of this useful feature.

### Pointer Declaration
In C++, a pointer is declared by specifying the data type it points to, followed by an asterisk (`*`) and the variable name. This creates a variable that can store the memory address of another variable of the specified data type.

For example, to declare a pointer that points to an integer variable, we can write:
```cpp
int *ptr;
```
This creates a pointer variable called `ptr` that can hold the memory address of an integer variable.

Similarly, to declare a pointer that points to a floating-point number variable or a character variable, we can write:
```cpp
float *floatPtr;
char *charPtr;
```
It is important to note that the `*` in the declaration is not an operator, but rather a part of the type specifier. This means that the type of the pointer is not the same as the type of the variable it points to.

Furthermore, it is possible to declare multiple pointers of the same data type on the same line, as long as each pointer is preceded by an asterisk:
```cpp
int *ptr1, *ptr2, *ptr3;
```

### Pointer Initialization
Initializing a pointer involves assigning it the address of the variable it is intended to point to. This can be done using the address-of operator (`&`). The address-of operator returns the memory address of the variable whose address is being sought.

Here's an example that demonstrates how to initialize a pointer:
```cpp
// Declare an integer variable named 'num' and assign it the value 10
int num = 10;

// Declare a pointer to an integer named 'ptr' and initialize it by assigning the address of the variable 'num'
int *ptr = &num;
```
In this example, the pointer `ptr` is initialized to point to the memory address of the variable `num`. The type of the pointer should match the type of the variable it is pointing to. In this case, `ptr` is an integer pointer because it is pointing to an integer variable, `num`.

### Dereferencing Pointers
Dereferencing pointers is a crucial operation in C++ that allows you to access the value stored at the memory location a pointer is pointing to. The process of dereferencing involves using the asterisk (`*`) operator, also known as the dereference operator, in conjunction with the pointer variable.
```cpp
int num = 10;
int *ptr = &num;
int value = *ptr; // value now contains 10
```

Here's a complete example:
```cpp
#include <iostream>

int main() {
    // Declare an integer variable named 'num' and assign it the value 10
    int num = 10;

    // Declare a pointer to an integer named 'ptr' and initialize it by assigning the address of the variable 'num'
    int *ptr = &num;

    // Print the value of 'num' and its memory address
    std::cout << "Value of num: " << num << std::endl;
    std::cout << "Memory address of num: " << &num << std::endl;

    // Print the value of 'ptr' and the value it points to
    std::cout << "Value of ptr (memory address of num): " << ptr << std::endl;
    std::cout << "Value pointed to by ptr: " << *ptr << std::endl;

    return 0;
}
```
In this example, we first declare and initialize an integer variable `num` and an integer pointer `ptr`. Then, we print the value of `num` and its memory address. Following that, we print the value of `ptr`, which is the memory address of `num`, and the value it points to, which is the value stored in `num`.

### Pointer Arithmetic
Pointer arithmetic is a powerful feature in C++ that allows you to perform arithmetic operations on pointers, such as addition, subtraction, increment (`++`), and decrement (`--`). These operations enable you to navigate through arrays and manipulate memory more efficiently. However, caution must be exercised when performing pointer arithmetic, as accessing memory outside the intended range can lead to undefined behavior and potential program crashes.

When performing arithmetic operations on pointers, the operations take the size of the data type the pointer points to into account. For instance, incrementing an integer pointer would advance it to the next integer in memory, taking into consideration the size of an integer on the specific platform.

Here's an example to demonstrate pointer arithmetic:
```cpp
int arr[5] = {1, 2, 3, 4, 5};
int *ptr = arr;

ptr++; // ptr now points to the second element of the array (2)
ptr--; // ptr now points back to the first element of the array (1)
ptr += 3; // ptr now points to the fourth element of the array (4)
ptr -= 2; // ptr now points to the second element of the array (2)
```

### Pointers and Arrays
In C++, pointers and arrays share a close relationship. The name of an array acts as a constant pointer to its first element, meaning you can use pointers and pointer arithmetic to access and manipulate the elements of an array. This connection allows for efficient navigation and operations on arrays.

Here's an example that demonstrates how to use pointers and pointer arithmetic to access array elements:
```cpp
#include <iostream>

int main() {
    // Declare and initialize an integer array with five elements
    int arr[5] = {10, 20, 30, 40, 50};

    // Declare a pointer to an integer named 'ptr' and initialize it with the address of the first element of the array 'arr'
    int *ptr = arr;

    // Use a for loop to iterate through the array elements using the pointer and pointer arithmetic
    for (int i = 0; i < 5; i++) {
        // Access the array element at the index 'i' by adding 'i' to the pointer and dereferencing the resulting address
        std::cout << "Element " << i << ": " << *(ptr + i) << std::endl;
    }

    return 0;
}
```
n this example, we first declare and initialize an integer array `arr` with five elements. Then, we declare and initialize a pointer `ptr` to point to the first element of the array. Inside the for loop, we use pointer arithmetic to access each element of the array by adding the loop index `i` to the pointer `ptr` and dereferencing the resulting address. This method allows us to access and print the value of each element in the array using the pointer.

> **Note**
>
> Using pointers in conjunction with arrays can lead to more efficient and flexible code, especially when working with dynamic memory allocation or multi-dimensional arrays. However, it is important to be cautious when performing pointer arithmetic to ensure that you do not access memory outside the boundaries of the array, as doing so can lead to undefined behavior and potential program crashes.

### Pointer to Pointer
A pointer can point to another pointer, creating what is known as a double pointer (or pointer to pointer). Double pointers are declared using two asterisks (`**`). Working with double pointers allows you to manage complex data structures, such as dynamically allocated multi-dimensional arrays or linked lists, with greater flexibility and efficiency.

Here's an example that demonstrates the use of a double pointer:
```cpp
#include <iostream>

int main() {
    // Declare an integer variable named 'num' and assign it the value 42
    int num = 42;

    // Declare a pointer to an integer named 'ptr' and initialize it by assigning the address of the variable 'num'
    int *ptr = &num;

    // Declare a double pointer to an integer named 'doublePtr' and initialize it by assigning the address of the pointer 'ptr'
    int **doublePtr = &ptr;

    // Print the value of 'num', the value pointed to by 'ptr', and the value pointed to by 'doublePtr'
    std::cout << "Value of num: " << num << std::endl;
    std::cout << "Value of *ptr: " << *ptr << std::endl;
    std::cout << "Value of **doublePtr: " << **doublePtr << std::endl;

    return 0;
}
```
In this example, we declare and initialize an integer variable `num`, an integer pointer `ptr`, and a double pointer `doublePtr`. By dereferencing `ptr`, we can access the value of `num`, and by dereferencing `doublePtr` twice, we can access the same value as well.

In the following example, we'll use an int data type, a pointer to an int, and a pointer to a pointer to an int. Then, we'll print their values to demonstrate their relationship.
```cpp
#include <iostream>

int main() {
    // Declare an int variable
    int num = 42;

    // Declare a pointer to an int and initialize it with the address of num
    int *numPtr = &num;

    // Declare a pointer to a pointer to an int and initialize it with the address of numPtr
    int **numPtrPtr = &numPtr;

    // Print the values and addresses of num, numPtr, and numPtrPtr
    std::cout << "num: " << num << ", address of num: " << &num << std::endl;
    std::cout << "numPtr: " << numPtr << ", address of numPtr: " << &numPtr << ", value pointed by numPtr: " << *numPtr << std::endl;
    std::cout << "numPtrPtr: " << numPtrPtr << ", address of numPtrPtr: " << &numPtrPtr << ", value pointed by numPtrPtr: " << *numPtrPtr << ", value pointed by value pointed by numPtrPtr: " << **numPtrPtr << std::endl;

    return 0;
}
```
When you run this program, you will see output similar to the following:
```cpp
num: 42, address of num: 0x7ffee5c5f78c
numPtr: 0x7ffee5c5f78c, address of numPtr: 0x7ffee5c5f780, value pointed by numPtr: 42
numPtrPtr: 0x7ffee5c5f780, address of numPtrPtr: 0x7ffee5c5f778, value pointed by numPtrPtr: 0x7ffee5c5f78c, value pointed by value pointed by numPtrPtr: 42
```
In the output, you can see that:
* The value of `num` is 42.
* The value of `numPtr` is the address of `num`, and the value pointed by `numPtr` is the value of `num` (42).
* The value of `numPtrPtr` is the address of `numPtr`, and the value pointed by `numPtrPtr` is the value of `numPtr` (which is the address of `num`). Finally, the value pointed by the value pointed by `numPtrPtr` is the value of `num` (42).

Here's a representation of the memory layout based on the example output shown above:
```md
| Address         | Value          | Description                  |
|-----------------|----------------|------------------------------|
| 0x7ffee5c5f78c  | 42             | num                          |
| 0x7ffee5c5f780  | 0x7ffee5c5f78c | numPtr (points to num)       |
| 0x7ffee5c5f778  | 0x7ffee5c5f780 | numPtrPtr (points to numPtr) |
```
This table shows the memory addresses and their corresponding values for `num`, `numPtr`, and `numPtrPtr`. The value of `numPtr` is the address of `num`, and the value of `numPtrPtr` is the address of `numPtr`.

### `const`
Pointers can be declared as `const` as well. Here is an example:
```cpp
#include <iostream>

int main() {
    int x = 5;
    const int* ptr = &x; // declare a const pointer to x

    // *ptr = 6; // this will cause a compiler error
    x = 6; // modifying x is still allowed

    std::cout << "x = " << x << ", *ptr = " << *ptr << std::endl;

    return 0;
}
```
In this example, we declare a non-const integer variable called `x` and initialize it to the value 5. We then declare a const pointer to `x` called `ptr`. This means that the value of `x` cannot be modified through `ptr`, but `x` itself can still be modified. We then try to modify the value of `*ptr`, which will cause a compiler error. Finally, we modify the value of `x` and print the values of `x` and `*ptr` to the console.

References can be declared as `const`. For example:
```cpp
#include <iostream>

int main() {
    int x = 5;
    const int& ref = x; // declare a const reference to x

    // ref = 6; // this will cause a compiler error
    x = 6; // modifying x is still allowed

    std::cout << "x = " << x << ", ref = " << ref << std::endl;

    return 0;
}
```
In this example, we declare a non-const integer variable called `x` and initialize it to the value 5. We then declare a `const` reference to `x` called `ref`. This means that the value of `x` cannot be modified through `ref`, but `x` itself can still be modified. We then try to modify the value of `ref`, which will cause a compiler error. Finally, we modify the value of `x` and print the values of `x` and `ref` to the console.

## Dynamic Memory Allocation, `new` and `delete`
Dynamic memory allocation is a technique that allows you to allocate memory during runtime. This is particularly useful when the amount of memory needed is unknown at compile time or when you need to change the size of the allocated memory during the execution of your program. In C++, dynamic memory allocation is typically done using the `new` and `delete` operators.

### `new`
The `new` operator is used to allocate memory on the heap for a specified data type or object. When memory is allocated using `new`, it is initialized according to the type, and the memory address is returned as a pointer to the allocated memory.

Here's an example of using the `new` operator to allocate memory for an integer:
```cpp
int *ptr = new int;
```
In this example, the `new` operator allocates memory for an integer on the heap, and the address of the allocated memory is stored in the integer pointer `ptr`.

### `delete`
The `delete` operator is used to deallocate memory that was previously allocated using the `new` operator. It is important to deallocate memory when it is no longer needed to prevent memory leaks in your program.

Here's an example of using the `delete` operator to deallocate memory allocated for an integer:
```cpp
delete ptr;
```
In this example, the `delete` operator deallocates the memory pointed to by the integer pointer `ptr`. After deallocating the memory, the pointer becomes a dangling pointer, and you should avoid using it without reassigning it to a valid memory address.

Here's a complete example that demonstrates dynamic memory allocation and deallocation for an integer:
```cpp
#include <iostream>

int main() {
    // Allocate memory for an integer using the 'new' operator
    int *ptr = new int;

    // Assign a value to the allocated memory
    *ptr = 42;

    // Print the value stored at the allocated memory
    std::cout << "Value of *ptr: " << *ptr << std::endl;

    // Deallocate the memory using the 'delete' operator
    delete ptr;

    return 0;
}
```

### Dynamic Memory Allocation for One-Dimentional Arrays
When allocating memory for arrays, you can use the `new` and `delete` operators along with the square brackets (`[]`) to specify the number of elements in the array.

Here's an example that demonstrates dynamic memory allocation and deallocation for an array:
```cpp
#include <iostream>

int main() {
    // Allocate memory for an array of 5 integers
    int *arr = new int[5];

    // Assign values to the array elements
    for (int i = 0; i < 5; i++) {
        arr[i] = i * 10;
    }

    // Print the values stored in the array
    for (int i = 0; i < 5; i++) {
        std::cout << "Element " << i << ": " << arr[i] << std::endl;
    }

    // Deallocate the memory for the array using the 'delete' operator
    delete[] arr;

    return 0;
}
```
In this example, we allocate memory for an array of 5 integers, assign values to the array elements, print the values, and then deallocate the memory using the `delete[]` operator. Note the use of square brackets in the `delete` operator when deallocating memory for an array.

Remember to always deallocate memory allocated with the `new` operator using the corresponding `delete` operator to prevent memory leaks in your program. Additionally, avoid accessing deallocated memory or memory that has not been initialized, as this can lead to undefined behavior and potential program crashes.

### Dynamic Memory Allocation for Two-Dimentional Arrays (Double Pointers)
When working with two-dimensional arrays in C++, dynamic memory allocation can be achieved using double pointers. This technique allows you to create flexible data structures, such as multi-dimensional arrays with varying sizes, which can be modified during runtime. To allocate memory for a two-dimensional array, you first allocate an array of pointers using the `new` operator, and then, for each pointer, allocate memory for the corresponding row or column. Double pointers are used to store the base address of the allocated memory, providing efficient access to individual elements in the array. When deallocating memory for a dynamically allocated two-dimensional array, you must ensure that the memory for each row or column is released first, followed by the memory for the array of pointers. The use of double pointers for dynamic memory allocation of two-dimensional arrays enables greater control over memory management, allowing programmers to optimize performance and resource usage for complex data structures and algorithms.

Now, let's look at another example, where we use double pointers to create a dynamic two-dimensional array:
```cpp
#include <iostream>

int main() {
    int rows = 3;
    int cols = 4;

    // Allocate memory for a two-dimensional array using double pointers
    int **arr = new int*[rows];
    for (int i = 0; i < rows; i++) {
        arr[i] = new int[cols];
    }

    // Fill the array with some values
    int count = 0;
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            arr[i][j] = count++;
        }
    }

    // Print the values in the two-dimensional array
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            std::cout << "Element (" << i << ", " << j << "): " << arr[i][j] << std::endl;
        }
    }

    // Deallocate the memory for the two-dimensional array
    for (int i = 0; i < rows; i++) {
        delete[] arr[i];
    }
    delete[] arr;

    return 0;
}
```
In this example, we use a double pointer `arr` to create a dynamic two-dimensional array with a specified number of rows and columns. We fill the array with values, print them, and then deallocate the memory at the end of the program. Double pointers are particularly useful in scenarios like this, where dynamic memory allocation and manipulation are required.

> **Note**
> 
> Dynamic memory allocation for two-dimensional arrays using double pointers can be extended to handle arrays with more dimensions, providing even greater flexibility in managing complex data structures. By employing a hierarchical approach to allocate memory for each dimension, you can create multi-dimensional arrays with varying sizes and adjust them during runtime as needed. This technique involves allocating memory for an array of pointers representing the highest dimension, then allocating memory for each subsequent dimension in a nested manner. Similarly, deallocation must be performed in a careful, hierarchical manner to ensure all the memory is properly released. The use of pointers to pointers (or even pointers to pointers to pointers, and so on) enables efficient access to individual elements within the multi-dimensional array. Employing dynamic memory allocation for multi-dimensional arrays allows programmers to tackle intricate problems and create sophisticated algorithms that require adaptable and intricate data structures, ultimately improving performance and resource utilization in a wide range of applications.

## Resizing Arrays
In C++, resizing arrays can be challenging because the size of the array is fixed at compile time, and you cannot change it directly during runtime. However, you can achieve resizing of arrays by using dynamic memory allocation and copying the contents to a newly allocated array with a different size. The C++ Standard Library also provides the `std::vector` container, which is a dynamic array that can automatically resize itself when needed. You will learn C++ Standard Library later in this bootcamp.

Here's an example of how you can resize an array using dynamic memory allocation:
```cpp
#include <iostream>
#include <cstring> // for std::memcpy

int main() {
    int original_size = 5;
    int new_size = 10;

    // Allocate memory for the original array
    int *arr = new int[original_size];

    // Assign values to the original array elements
    for (int i = 0; i < original_size; i++) {
        arr[i] = i * 10;
    }

    // Allocate memory for the new resized array
    int *resized_arr = new int[new_size];

    // Copy the elements from the original array to the resized array
    std::memcpy(resized_arr, arr, original_size * sizeof(int));

    // Assign new values to the additional elements in the resized array
    for (int i = original_size; i < new_size; i++) {
        resized_arr[i] = i * 10;
    }

    // Deallocate memory for the original array
    delete[] arr;

    // Update the pointer to point to the resized array
    arr = resized_arr;

    // Print the values stored in the resized array
    for (int i = 0; i < new_size; i++) {
        std::cout << "Element " << i << ": " << arr[i] << std::endl;
    }

    // Deallocate memory for the resized array
    delete[] arr;

    return 0;
}
```
In this example, we first allocate memory for an integer array `arr` with an `original_size` of 5 elements. We then allocate memory for a new integer array `resized_arr` with a `new_size` of 10 elements. We use the `std::memcpy` function to copy the elements from the original array to the resized array. After copying the elements, we deallocate the memory for the original array and update the pointer `arr` to point to the resized array. Finally, we print the values stored in the resized array and deallocate its memory.