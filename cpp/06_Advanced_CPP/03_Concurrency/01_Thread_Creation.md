## Introduction to Multithreading
### Concept of Threads in Computing
In computing, a thread refers to a sequence of instructions that can be executed independently of other threads. Threads allow for concurrent execution and can perform tasks concurrently, enabling parallelism in programs. Threads share the same memory space within a process, making it easier to communicate and synchronize data between them.

### Benefits and Use Cases of Multithreading
Multithreading offers several advantages, including:

* **Improved performance**: By utilizing multiple threads, a program can execute multiple tasks simultaneously, leveraging the available CPU cores and speeding up execution.
* **Enhanced responsiveness**: Multithreading allows applications to remain responsive during resource-intensive tasks by offloading them to separate threads.
* **Modularity**: Threads enable the division of complex tasks into smaller, more manageable units, facilitating modular and maintainable code.

### Comparison of Processes and Threads
Processes and threads are both units of execution, but they have some key differences. Processes are independent instances of programs, while threads are lighter-weight units that exist within a process. Here are some differences:

* **Memory**: Processes have separate memory spaces, while threads share memory within a process.
* **Creation Overhead**: Creating a process is more resource-intensive compared to creating a thread.
* **Communication**: Inter-process communication is more complex than inter-thread communication due to the need for explicit mechanisms like message passing or shared memory.
* **Context Switching**: Context switching between processes is typically slower than switching between threads.

## Creating Threads in C++ (C++11 onwards)
### Overview of `std::thread`
The `std::thread` class in C++ provides a way to create and manage threads. It allows you to execute a function concurrently in a separate thread of execution.

### Syntax and Usage of `std::thread`
* **Creation**: To create a thread, you pass a callable object (such as a function or lambda) to the `std::thread` constructor.
* **Joining**: The `join()` member function is used to wait for the thread to finish execution before proceeding.
* **Detaching**: Alternatively, you can call the `detach()` member function to detach the thread, allowing it to execute independently.
* **Thread Identifiers**: Each `std::thread` object has an associated thread ID, which can be obtained using the `get_id()` member function.

Example:
```cpp
#include <iostream>
#include <thread>

// Function to be executed by the thread
void threadFunction()
{
    std::cout << "Thread function executing\n";
}

int main()
{
    // Creating a thread
    std::thread threadObj(threadFunction);

    // Main thread execution
    std::cout << "Main function executing\n";

    // Wait for the thread to finish
    threadObj.join();

    // Get the thread ID
    std::cout << "Thread ID: " << threadObj.get_id() << std::endl;

    return 0;
}
```
In this example, we have a function called `threadFunction` that does not take any arguments. We want to execute this function in a separate thread.

In the `main` function, we create a thread object named `threadObj` using the `std::thread` constructor. We pass the `threadFunction` as the argument to the constructor. This creates a new thread of execution and starts running the `threadFunction`.

Next, in the main thread, we output the message "Main function executing" to indicate the execution of the main thread.

To ensure that the main thread waits for the newly created thread to finish its execution, we call the `join()` function on the `threadObj`. This function blocks the execution of the main thread until the thread represented by `threadObj` completes its execution.

After the `join()` call, we obtain the thread ID of `threadObj` using the `get_id()` member function. The thread ID is a unique identifier associated with the thread. We output this thread ID using `std::cout`.

Finally, we return 0 to indicate successful program execution.

When you run this code, you will see the following output:
```cpp
Main function executing
Thread function executing
Thread ID: [thread ID]
```
The main thread executes first and prints "Main function executing." Then, the separate thread executes and prints "Thread function executing." Finally, the thread ID is printed, which is a unique identifier for the thread.

### Passing Arguments to Thread Functions
You can pass arguments to the thread function by providing them as additional arguments to the `std::thread` constructor. You can pass arguments by value or by reference using `std::ref()`.

Example:
```cpp
#include <iostream>
#include <thread>

// Function to be executed by the thread
void threadFunction(int value)
{
    std::cout << "Thread function executing with value: " << value << std::endl;
}

int main()
{
    int data = 42;

    // Creating a thread with argument
    std::thread threadObj(threadFunction, data);

    // Main thread execution
    std::cout << "Main function executing\n";

    // Wait for the thread to finish
    threadObj.join();

    return 0;
}
```
The key difference in this example is the addition of an integer variable `data` and passing it as an argument to the `threadFunction`.

In the `main` function, we declare an integer variable `data` and initialize it with the value 42. This variable serves as an argument that will be passed to the `threadFunction`.

When creating the thread using `std::thread threadObj(threadFunction, data);`, we provide `threadFunction` as the first argument and data as the second argument. This indicates that the `threadFunction` will be executed with the value of data as its parameter.

Inside the `threadFunction`, we print "Thread function executing with value: " followed by the value parameter passed to the function.

When the program is executed, you will see the following output:
```cpp
Main function executing
Thread function executing with value: 42
```
The main thread executes first and prints "Main function executing." Then, the separate thread executes and prints "Thread function executing with value: 42," indicating that the `threadFunction` was executed with the provided value.

### Handling Exceptions in Threads
Exceptions thrown in a thread can terminate the entire program if they are not caught within the thread. To handle exceptions, you can wrap the thread's function body in a `try-catch` block or use a lambda function.

Example:
```cpp
#include <iostream>
#include <thread>

// Function to be executed by the thread
void threadFunction()
{
    try {
        throw std::runtime_error("Exception from thread");
    } catch (const std::exception& ex) {
        std::cout << "Exception caught: " << ex.what() << std::endl;
    }
}

int main()
{
    // Creating a thread
    std::thread threadObj(threadFunction);

    // Main thread execution
    std::cout << "Main function executing\n";
    // Wait for the thread to finish
    threadObj.join();

    return 0;
}
```
In this example and within the `threadFunction`, we intentionally throw an exception using `throw std::runtime_error("Exception from thread")`. This simulates an exception occurring in the thread.

To handle the exception, we wrap the `throw` statement within a `try-catch` block. In the catch block, we catch the exception by reference as a `const std::exception&` and print out the error message using `ex.what()`.

In the `main` function, we create a thread named `threadObj` using the `std::thread` constructor and pass `threadFunction` as the argument.

The main thread continues its execution after creating the thread and outputs "Main function executing".

To ensure that the main thread waits for the thread to finish, we call `threadObj.join()`. This function blocks the main thread until the thread represented by `threadObj` completes its execution.

When the exception is thrown in the thread, it is caught in the `catch` block of the `threadFunction`, and the corresponding error message is printed.

Upon running the program, you will see the following output:
```cpp
Main function executing
Exception caught: Exception from thread
```
The main thread executes first, prints "Main function executing", and then waits for the separate thread to finish. The separate thread executes its code and throws an exception, which is caught in the catch block. The error message "Exception caught: Exception from thread" is printed to indicate the exception handling.