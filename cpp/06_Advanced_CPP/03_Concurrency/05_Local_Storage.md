## Thread Local Storage (C++11 onwards)
### Overview of `thread_local` Keyword
The `thread_local` keyword in C++ allows the creation of variables that are local to each thread. Each thread has its own copy of the variable, ensuring thread isolation and avoiding data races.

Example:
```cpp
#include <iostream>
#include <thread>

// Function to be executed by the thread
void printThreadID()
{
    static thread_local int threadID = 0; // Thread-local variable

    // Generate a unique ID for each thread
    threadID++;

    std::cout << "Thread ID: " << threadID << std::endl;
}

int main()
{
    std::thread thread1(printThreadID);
    std::thread thread2(printThreadID);

    thread1.join();
    thread2.join();

    return 0;
}
```
In this example, we have a function `printThreadID` that prints the ID of each thread. We use the `thread_local` keyword to declare a thread-local variable named `threadID`. Each thread will have its own copy of this variable.

Inside the function, we increment the `threadID` to generate a unique ID for each thread and then print it.

We create two threads, `thread1` and `thread2`, that call the `printThreadID` function. Each thread will have its own copy of the `threadID` variable.

When you run this code, you will see the following output:
```cpp
Thread ID: 1
Thread ID: 1
```
Since each thread has its own copy of the threadID variable, they generate and print unique thread IDs independently. In this case, both threads have a threadID value of 1 because the variable is initialized to 0 for each thread.

### Use Cases for Thread Local Storage (Per-Thread Data, Random Number Generators)
Thread Local Storage is useful for scenarios where you need to maintain per-thread data or have thread-specific instances of objects such as random number generators.

#### Per-Thread Data
Thread Local Storage allows you to store per-thread data that is isolated from other threads. Each thread can have its own set of data that is accessible only to that thread.

Example:
```cpp
#include <iostream>
#include <thread>
#include <vector>

thread_local std::vector<int> threadData; // Thread-local data

// Function to be executed by the thread
void addToThreadData(int value)
{
    threadData.push_back(value);
}

int main()
{
    std::thread thread1(addToThreadData, 10);
    std::thread thread2(addToThreadData, 20);

    thread1.join();
    thread2.join();

    std::cout << "Thread 1 Data: ";
    for (const auto& value : threadData) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    std::cout << "Thread 2 Data: ";
    for (const auto& value : threadData) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```
In this example, we have a `thread_local` vector named `threadData` that represents per-thread data. Each thread will have its own vector to store data.

We have a function `addToThreadData` that adds a value to the `threadData` vector. Each thread will push its own value to its specific vector.

We create two threads, `thread1` and `thread2`, that call the `addToThreadData` function with different values.

After both threads have finished their execution, we print the data stored in the `threadData` vector for each thread.

When you run this code, you will see the following output:
```cpp
Thread 1 Data: 10
Thread 2 Data: 20
```
Since each thread has its own `threadData` vector, the values added by each thread are stored separately. In this case, thread 1 adds the value 10, and thread 2 adds the value 20. The data is isolated for each thread, and accessing `threadData` from one thread does not interfere with the data of other threads.

### Random Number Generators
Thread Local Storage can be used to create thread-specific instances of random number generators. This ensures that each thread has its own random number generator and avoids contention or synchronization issues.

Example:
```cpp
#include <iostream>
#include <random>
#include <thread>

// Function to be executed by the thread
void generateRandomNumbers()
{
    thread_local std::random_device rd; // Thread-local random device
    thread_local std::mt19937 gen(rd()); // Thread-local random number generator

    std::uniform_int_distribution<int> distribution(1, 100);

    // Generate and print a random number
    int randomNum = distribution(gen);
    std::cout << "Random Number: " << randomNum << std::endl;
}

int main()
{
    std::thread thread1(generateRandomNumbers);
    std::thread thread2(generateRandomNumbers);

    thread1.join();
    thread2.join();

    return 0;
}
```
In this example, we have a function `generateRandomNumbers` that generates and prints a random number. We use `thread_local` to declare thread-local instances of the random device (`rd`) and the Mersenne Twister random number generator (`gen`).

Each thread will have its own random device and random number generator, ensuring that the generated numbers are independent and not influenced by other threads.

We create two threads, `thread1` and `thread2`, that call the `generateRandomNumbers` function.

When you run this code, you will see the following output:
```cpp
Random Number: ...
Random Number: ...
```
Each thread generates and prints its own random number independently. The thread-local instances of the random device and generator ensure that each thread has its own source of randomness and avoids contention or synchronization issues.

Thread Local Storage provides a convenient mechanism to store per-thread data or have thread-specific instances of objects. It ensures thread isolation and avoids data races by providing each thread with its own copy of the thread-local variable. This feature is useful in scenarios where you need per-thread data or want to maintain independent instances of objects across threads.

