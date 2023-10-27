## Atomic Operations (C++11 onwards)
### Overview of `std::atomic`
`std::atomic` provides a way to perform atomic operations on shared variables without the need for explicit locking. Atomic operations are thread-safe and ensure that concurrent accesses to the variable do not result in data races.

Example:
```cpp
#include <iostream>
#include <thread>
#include <atomic>

std::atomic<int> counter(0);

// Function to be executed by the thread
void incrementCounter()
{
    for (int i = 0; i < 100000; ++i) {
        counter++; // Atomic increment operation
    }
}

int main()
{
    std::thread thread1(incrementCounter);
    std::thread thread2(incrementCounter);

    thread1.join();
    thread2.join();

    std::cout << "Counter value: " << counter << std::endl;

    return 0;
}
```
In this example, we have an `std::atomic` variable named `counter` that is initialized to 0. The `std::atomic` type ensures that the increment operation `counter++` is performed atomically, preventing data races.

We create two threads, `thread1` and `thread2`, that call the `incrementCounter` function. Inside the function, each thread increments the `counter` variable by 1 for a total of 100,000 times.

After both threads have finished their execution, we print the final value of the `counter` variable.

When you run this code, you will see the following output:
```cpp
Counter value: 200000
```
The atomic increment operation `counter++` ensures that the updates to the `counter` variable are performed atomically, without data races. As a result, the final value of the `counter` variable is the expected sum of 200,000.

### Use Cases for Atomic Operations (Lock-Free Programming, Counters)
Atomic operations are useful in scenarios where multiple threads access and modify a shared variable concurrently. They provide a lock-free mechanism to ensure thread safety and prevent data races.

#### Lock-Free Programming
In lock-free programming, threads operate on shared variables without explicit locking mechanisms, such as mutexes. Atomic operations enable thread-safe access and modification of shared data without the need for explicit synchronization.

Example:
```cpp
#include <iostream>
#include <thread>
#include <atomic>

std::atomic<int> sharedData(0);

// Function to be executed by the thread
void modifyData()
{
    for (int i = 0; i < 100000; ++i) {
        sharedData.fetch_add(1, std::memory_order_relaxed); // Atomic fetch-and-add operation
    }
}

int main()
{
    std::thread thread1(modifyData);
    std::thread thread2(modifyData);

    thread1.join();
    thread2.join();

    std::cout << "Shared Data value: " << sharedData << std::endl;

    return 0;
}
```
In this example, we have an `std::atomic` variable named `sharedData` that is initialized to 0. The `std::atomic` type ensures that the fetch-and-add operation `sharedData.fetch_add(1)` is performed atomically, without data races.

We create two threads, `thread1` and `thread2`, that call the `modifyData` function. Inside the function, each thread performs a fetch-and-add operation on the `sharedData` variable by adding 1 to it for a total of 100,000 times.

After both threads have finished their execution, we print the final value of the `sharedData` variable.

When you run this code, you will see the following output:
```cpp
Shared Data value: 200000
```
The atomic fetch-and-add operation `sharedData.fetch_add(1)` ensures that the updates to the `sharedData` variable are performed atomically, without data races. As a result, the final value of the `sharedData` variable is the expected sum of 200,000.

#### Counters
Atomic operations are commonly used for implementing counters, where multiple threads increment or decrement a shared variable in a thread-safe manner.

Example:
```cpp
#include <iostream>
#include <thread>
#include <atomic>

std::atomic<int> counter(0);

// Function to be executed by the thread
void incrementCounter()
{
    for (int i = 0; i < 100000; ++i) {
        counter++; // Atomic increment operation
    }
}

void decrementCounter()
{
    for (int i = 0; i < 100000; ++i) {
        counter--; // Atomic decrement operation
    }
}

int main()
{
    std::thread thread1(incrementCounter);
    std::thread thread2(decrementCounter);

    thread1.join();
    thread2.join();

    std::cout << "Counter value: " << counter << std::endl;

    return 0;
}
```
In this example, we have an `std::atomic` variable named `counter` that is initialized to 0. The `std::atomic` type ensures that the increment and decrement operations (`counter++` and `counter--`) are performed atomically, without data races.

We create two threads, `thread1` and `thread2`, where `thread1` increments the counter variable by 1, and `thread2` decrements it by 1. Both threads perform their respective operations 100,000 times.

After both threads have finished their execution, we print the final value of the counter variable.

When you run this code, you will see the following output:
```cpp
Counter value: 0
```
Since the increment and decrement operations are balanced, the final value of the `counter` variable is 0. The atomic operations ensure that the updates to the counter variable are performed atomically, preventing data races.

Atomic operations provide a thread-safe and lock-free mechanism for accessing and modifying shared variables. They are particularly useful in scenarios where multiple threads operate on the same data concurrently. By using atomic operations, you can ensure correct and efficient access to shared data without the need for explicit locking mechanisms.