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

### Use Cases for Atomic Operations (Lock-Free Programming, Counters)
Atomic operations are useful in scenarios where multiple threads access and modify a shared variable concurrently. They provide a lock-free mechanism to ensure thread safety and prevent data races.


#### Lock-Free Programming
Lock-free programming allows threads to interact with shared variables without the traditional locking mechanisms, such as mutexes. This is achieved using atomic operations, which ensure thread-safe access and modification of shared data without explicit synchronization.

Example:
```cpp
#include <iostream>
#include <thread>
#include <atomic>

std::atomic<bool> flag(false); // Atomic flag to indicate data availability
std::atomic<int> sharedData(0); // Shared atomic data

// Producer function to be executed by one thread
void produceData()
{
    for (int i = 1; i <= 5; ++i) {
        while (flag.load(std::memory_order_acquire)); // Waits until data is consumed
        sharedData.store(i, std::memory_order_relaxed); // Atomic store operation
        std::cout << "Produced: " << i << std::endl;
        flag.store(true, std::memory_order_release); // Indicates data availability
    }
}

// Consumer function to be executed by another thread
void consumeData()
{
    for (int i = 1; i <= 5; ++i) {
        while (!flag.load(std::memory_order_acquire)); // Waits for data to be available
        int data = sharedData.load(std::memory_order_relaxed); // Atomic load operation
        std::cout << "Consumed: " << data << std::endl;
        flag.store(false, std::memory_order_release); // Indicates data consumption
    }
}

int main()
{
    std::thread producer(produceData);
    std::thread consumer(consumeData);

    producer.join();
    consumer.join();

    return 0;
}
```
In this example, we have a producer-consumer scenario. The `produceData` function produces data and sets an atomic flag `flag` to indicate data availability. The `consumeData` function waits for the flag to be set before consuming the data. Both functions use atomic operations to ensure thread-safe access to the shared data and flag without the need for explicit locks.

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

Atomic operations provide a thread-safe and lock-free mechanism for accessing and modifying shared variables. They are particularly useful in scenarios where multiple threads operate on the same data concurrently. 