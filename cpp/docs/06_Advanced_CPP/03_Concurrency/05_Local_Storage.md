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

    // Generates a unique ID for each thread
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
In this example, we have a function `printThreadID` that prints the ID of each thread. We use the `thread_local` keyword to declare a thread-local variable named `threadID`. 

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
Thread Local Storage (TLS) provides a mechanism to store data that is specific to individual threads. This ensures that each thread has its own isolated data, preventing interference from other threads.

Example:
```cpp
#include <iostream>
#include <thread>

thread_local int threadData; // Thread-local data

// Function to be executed by the thread
void addToThreadData(int value)
{
    threadData = value;
    std::cout << "Thread " << std::this_thread::get_id() << " Data: " << threadData << std::endl;
}

int main()
{
    std::thread thread1(addToThreadData, 10);
    std::thread thread2(addToThreadData, 20);

    thread1.join();
    thread2.join();

    return 0;
}
```

In this example, we use a `thread_local` integer named `threadData` to represent the per-thread data. Each thread will have its own distinct value for this variable.

The function `addToThreadData` assigns a value to the `threadData` variable and then prints it. This ensures that each thread's data is displayed within the context of that thread.

Upon execution, two threads, `thread1` and `thread2`, are created. Each thread invokes the `addToThreadData` function with distinct values.

The expected output will resemble:
```cpp
Thread [thread1's ID] Data: 10
Thread [thread2's ID] Data: 20
```

The exact thread IDs will vary with each run. However, the key takeaway is that each thread has its own isolated data, ensuring that the operations of one thread do not affect the data of another.

### Pseudo Random Number Generators (PRNGs)
Thread Local Storage can be used to create thread-specific instances of pseudo random number generators. This ensures that each thread has its own random number generator and avoids contention or synchronization issues.

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

    // Generates and prints a random number
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

Thread Local Storage provides a convenient mechanism to store per-thread data or have thread-specific instances of objects. It ensures thread isolation and avoids data races by providing each thread with its own copy of the thread-local variable. This feature is useful in scenarios where you need per-thread data or want to maintain independent instances of objects across threads.

