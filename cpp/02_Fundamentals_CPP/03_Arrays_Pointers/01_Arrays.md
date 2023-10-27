## Introduction to Arrays
In C++, an array is a collection of elements of the same data type that are stored in a contiguous block of memory. The elements of an array can be accessed and manipulated by their position, or index, in the array. Arrays are a fundamental data structure in C++ that you will encounter frequently in programming.

Arrays are useful for storing and accessing collections of data, such as a list of student grades or a set of sensor readings from an experiment. They can also be used to efficiently perform operations on large amounts of data, such as sorting or searching.

### Declaring an Array
An array is defined by specifying the data type of its elements and the number of elements it contains. For example, an array of integers with five elements would be declared as follows:
```cpp
int myArray[5];
```
This creates an integer array named `myArray` with five elements. The elements of the array can be accessed using their index, which starts at `0` and goes up to one less than the number of elements in the array.

### Initializing an Array
An array can be initialized at the time of declaration by providing a list of values enclosed in braces. For example, to initialize an array of integers with the values 1, 2, 3, 4, and 5, we would use the following syntax:
```cpp
int myArray[5] = {1, 2, 3, 4, 5};
```
If the number of values provided is less than the number of elements in the array, the remaining elements will be initialized to their default value (0 for integers). For example:
```cpp
int myArray[5] = {1, 2, 3};
```
This creates an array of integers with five elements, initialized to the values 1, 2, 3, 0, and 0.

In the following example, we declare and initialize an array without mentioning its size:
```cpp
int myArray[] = {1, 2, 3, 4, 5};
```
An integer array named `myArray` with five elements is declared. The elements are specified within braces and separated by commas.

Here is another example on declaring and initializing an array without mentioning its size:
```cpp
int myArray4[] {1, 2, 3, 4, 5};
```
> **Note** 
> 
> In C++, there is no difference between declaring an array as, for example, `int myArray[] {1, 2, 3};` and `int myArray[] = {1, 2, 3};`. Both forms are used for array initialization, and they produce the same result.
> 
> The only difference between these two forms is the syntax used to initialize the array. The first form uses uniform initialization syntax with braces `{}`, which was introduced in C++11, while the second form uses an older syntax with an equal sign `=`.
> 
> In general, the uniform initialization syntax is preferred over the older syntax, as it provides better type safety and consistency across different types of initialization. For example, uniform initialization syntax can also be used to initialize non-array objects, such as structs and classes, in a consistent and intuitive way.

### Accessing Array Elements
The elements of an array can be accessed using their index. The index starts at 0 for the first element and goes up to one less than the number of elements in the array. For example, to access the first element of the array, we would use the following syntax:
```cpp
int firstElement = myArray[0];
```

### Modifying Array Elements
Array elements can be modified using their index. For example, to set the second element of the array to the value 10, we would use the following syntax:
```cpp
myArray[1] = 10;
```

Here is an example program that demonstrates the declaration, initialization, and manipulation of an array of integers:
```cpp
#include <iostream>

using namespace std;

int main() {
    // Declare and initialize an array of integers
    int myArray[5] = {1, 2, 3, 4, 5};

    // Print the array elements
    for (int i = 0; i < 5; i++) {
        cout << "Element " << i << " = " << myArray[i] << endl;
    }

    // Modify the third element of the array
    myArray[2] = 10;

    // Print the modified array elements
    for (int i = 0; i < 5; i++) {
        cout << "Element " << i << " = " << myArray[i] << endl;
    }

    return 0;
}
```
This program demonstrates the use of arrays. Firstly, an integer array named `myArray` is declared and initialized with five elements having the values 1, 2, 3, 4, and 5. Then, a `for` loop is used to print each element of the array along with its index using `cout` statement. Next, the third element of the array is modified by setting its value to 10 using the index. Finally, another `for` loop is used to print the modified elements of the array. The program then returns 0, indicating successful execution.

### Array Bounds Checking
In C++, array bounds checking is not performed by default, which means that the program can access elements outside the bounds of an array without any warning or error message. This can result in unexpected behavior or even crashes if the program attempts to access invalid memory locations.

To perform array bounds checking in C++, we can manually check the index before accessing the array element. Here is an example of using a loop to check the bounds of an array:
```cpp
#include <iostream>

using namespace std;

int main() {
    int myArray[5] = {1, 2, 3, 4, 5};
    int index;

    cout << "Enter an index to access the array element: ";
    cin >> index;

    if (index >= 0 && index < 5) {
        cout << "Element " << index << " = " << myArray[index] << endl;
    } else {
        cout << "Error: index is out of range." << endl;
    }

    return 0;
}
```
In this example, we declare and initialize an array of integers named `myArray` with the values 1, 2, 3, 4, and 5. We then prompt the user to enter an index to access the array element. Before accessing the element, we check whether the `index` is within the valid range of 0 to 4 using an if statement. If the `index` is within range, we print the corresponding element of the array. Otherwise, we print an error message indicating that the `index` is out of range.

> **Note**
>
> It's worth noting that while manual bounds checking is a viable option for small arrays, it can become impractical and error-prone for larger arrays or more complex programs. For this reason, C++ provides advanced features such as the Standard Template Library (STL) containers and smart pointers, which can perform automatic bounds checking and memory management. These topics are covered later in this bootcamp.

### Determining the Size of Arrays
In C++, we can determine the size of an array using the `std::size` function provided by the `<iterator>` header. The `std::size` function returns the number of elements in an array, regardless of its type or size.

Here's an example of using the `std::size` function to determine the size of an integer array named `myArray`:
```cpp
#include <iostream>
#include <iterator>

int main() {
    int myArray[] = {1, 2, 3, 4, 5};
    int myArraySize = std::size(myArray);

    std::cout << "Number of elements in myArray: " << myArraySize << std::endl;

    return 0;
}
```
In this example, we declare and initialize an integer array named `myArray` with five elements. We then use the `std::size` function to determine the number of elements in the array, and assign the result to the variable `myArraySize`. Finally, we print the value of `myArraySize` to the console.

The output of this program will be:
```cpp
Number of elements in myArray: 5
```

Note that the `std::size` function requires C++17 or later, so make sure that your compiler supports this feature if you plan to use it. If your compiler doesn't support C++17 yet, you can use the `sizeof` operator to determine the size of the array.

When used with an array, the `sizeof` operator returns the total size in bytes of the array. To determine the number of elements in the array, we can divide the total size by the size of each element. For example, to determine the number of elements in an integer array named `myArray`, we can use the following expression:
```cpp
int myArraySize = sizeof(myArray) / sizeof(int);
```
In this expression, we divide the total size of the array `myArray` in bytes by the size of an `integer`, which is also in bytes. The resulting value is the number of elements in the array.

<!-- It's important to note that the `sizeof` operator can only determine the size of arrays that are declared with a fixed size. For arrays that are dynamically allocated using new or malloc, we need to keep track of the size separately.

It's also worth noting that the sizeof operator can return unexpected results if used with arrays that have been passed to a function, since arrays passed to functions decay to pointers. In this case, the sizeof operator returns the size of the pointer, not the size of the array. To avoid this issue, we can pass the size of the array as a separate argument to the function. -->

## Multi-Dimensional Arrays
In C++, a multi-dimensional array is an array with more than one dimension, also known as a matrix or a two-dimensional array. Multi-dimensional arrays are useful for representing tables of data, images, and other complex structures. In this lecture, we will discuss how to declare and use multi-dimensional arrays in C++.

### Declaring a Multi-dimensional Array
To declare a multi-dimensional array in C++, we use the following syntax:
```cpp
data_type array_name[size1][size2]...[sizeN];
```
where `data_type` is the type of the elements in the array, `array_name` is the name of the array, and `size1`, `size2`, ..., `sizeN` are the sizes of each dimension of the array. For example, to declare a 3x3 matrix of integers, we can use the following declaration:
```cpp
int matrix[3][3];
```
This declaration creates a multi-dimensional array named `matrix` with two dimensions, each with a size of 3.

### Initializing a Multi-dimensional Array
Multi-dimensional arrays can be initialized using nested braces `{}` to specify the values of each element in the array. For example, to initialize a 3x3 matrix of integers with the values 1 to 9, we can use the following initialization:
```cpp
int matrix[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```
This initialization creates a multi-dimensional array named `matrix` with two dimensions, each with a size of 3, and initializes each element with the corresponding value.

### Accessing Elements in a Multi-dimensional Array
To access an element in a multi-dimensional array, we use the following syntax:
```cpp
array_name[index1][index2]...[indexN]
```
where `array_name` is the name of the array, and `index1`, `index2`, ..., `indexN` are the indices of the element in each dimension of the array. For example, to access the element in the second row and third column of the `matrix` array declared above, we can use the following syntax:
```cpp
int element = matrix[1][2];
```
This syntax accesses the element in the second row (index 1) and third column (index 2) of the `matrix` array and assigns its value to the variable element.

Here are some examples of working with multi-dimensional arrays in C++:

#### Example 1: Summing Elements of a Matrix
Summing elements of a matrix means to add up all the values of the elements in the matrix. This is a common operation that can be used to compute various properties of the matrix, such as its total value, average value, or maximum value. Here is a sample C++ program on this:
```cpp
#include <iostream>

int main() {
    int matrix[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int sum = 0;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            sum += matrix[i][j];
        }
    }

    std::cout << "Sum of matrix elements: " << sum << std::endl;

    return 0;
}
```
In this example, we declare and initialize a 3x3 matrix named `matrix` with the values 1 to 9. We then use two nested loops to iterate over each element in the matrix and compute the sum of all its elements. Finally, we print the sum to the console.

#### Example 2: Transposing a Matrix
Transposing a matrix means to interchange its rows and columns. In other words, if we have a matrix `A` with dimensions `m x n`, we can create a new matrix `B` with dimensions `n x m`, where the element at row `i` and column `j` of matrix `B` is equal to the element at row `j` and column `i` of matrix `A`. Here is a sample C++ program:
```cpp
#include <iostream>

int main() {
    int matrix[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    std::cout << "Original matrix:" << std::endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << matrix[i][j] << " ";
        }
        std::cout << std::endl;
    }

    int transpose[3][3];
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matrix[i][j];
        }
    }

    std::cout << "Transposed matrix:" << std::endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << transpose[i][j] << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```
In this example, we declare and initialize a 3x3 matrix named `matrix` with the values 1 to 9. We then print the original matrix to the console using two nested loops. We then declare another 3x3 matrix named `transpose` and use two nested loops to compute its elements by transposing the elements of the original matrix. Finally, we print the transposed matrix to the console using two nested loops.

## Enum
In C++, an enum is a user-defined type that represents a set of named values. Enums can be used to improve the readability and maintainability of code by providing a clear and concise way to represent a fixed set of values.

### Defining an Enum
An enum is defined using the enum keyword followed by the name of the enum and its possible values enclosed in curly braces. Here is an example of defining an enum that represents the days of the week:
```cpp
enum DaysOfWeek {
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
};
```
In this example, we define an enum named `DaysOfWeek` with seven possible values representing the days of the week. By default, the first value is assigned the value 0, the second value is assigned the value 1, and so on. However, we can assign custom integer values to each enum value if we want:
```cpp
enum DaysOfWeek {
    Monday = 1,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
};
```
In this example, we assign the value 1 to Monday, and the subsequent values are assigned the next integer values in sequence.

### Using an Enum
Once an enum is defined, we can use it to represent values of that type. Here is an example of declaring a variable of the `DaysOfWeek` enum type and assigning it a value:
```cpp
DaysOfWeek today = Monday;
```
In this example, we declare a variable named `today` of the `DaysOfWeek` enum type and initialize it with the value `Monday`. We can then use this variable in expressions and statements just like any other variable:
```cpp
if (today == Saturday || today == Sunday) {
    cout << "It's the weekend!" << endl;
} else {
    cout << "It's a weekday." << endl;
}
```
In this example, we use the `today` variable in an if statement to check whether it represents a weekend day.

### Benefits of Enums
Enums provide several benefits over using integer or string literals to represent fixed sets of values:

* Readability: Enums provide a clear and concise way to represent a fixed set of values, which makes code easier to read and understand.

* Type safety: Enums are a distinct type in C++, which means that they cannot be mixed with other types. This helps prevent errors caused by accidentally assigning an incorrect value to a variable.

* Compile-time checking: Since enums are defined at compile time, the compiler can check for errors such as duplicate or undefined values.

* Maintainability: If the set of values represented by an enum changes, we only need to update the enum definition rather than updating every occurrence of the old values throughout the code.
