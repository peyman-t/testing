## Thread Synchronization
### Concept of Race Conditions and the Need for Synchronization
Race conditions occur when multiple threads access and modify shared data simultaneously, leading to unpredictable and incorrect results. Synchronization mechanisms are used to coordinate the execution of threads to avoid race conditions and ensure data integrity.

Example:
```cpp
#include <iostream>
#include <thread>

int counter = 0; // Shared variable

// Function to be executed by the thread
void incrementCounter()
{
    for (int i = 0; i < 100000; ++i) {
        counter++; // Access and modify shared data
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
In this example, we have a shared variable `counter`, and two threads `thread1` and `thread2` that increment the counter in a loop. However, since the threads access and modify the shared variable concurrently, a race condition occurs.

### Using `std::mutex` for Mutual Exclusion
`std::mutex` provides a mechanism for mutual exclusion, allowing only one thread to access a shared resource at a time. It ensures that only one thread can acquire the lock associated with the mutex and proceed while other threads are blocked.

Example:
```cpp
#include <iostream>
#include <thread>
#include <mutex>

int counter = 0; // Shared variable
std::mutex mutexObj; // Mutex for synchronization

// Function to be executed by the thread
void incrementCounter()
{
    for (int i = 0; i < 100000; ++i) {
        std::lock_guard<std::mutex> lock(mutexObj); // Lock the mutex
        counter++; // Access and modify shared data
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
In this example, we introduce a `std::mutex` named `mutexObj` for mutual exclusion. The `std::lock_guard` is used to acquire and release the lock automatically. By locking the mutex before accessing the shared variable `counter`, we ensure that only one thread can modify it at a time, preventing race conditions.

### Locking Strategies (`std::lock`, `std::lock_guard`, `std::unique_lock`)

`std::lock`, `std::lock_guard`, and `std::unique_lock` are synchronization primitives used for locking and unlocking mutexes.

* `std::lock`: Locks multiple mutexes simultaneously to avoid deadlock by acquiring locks in a deadlock-free manner.
* `std::lock_guard`: Provides a convenient way to acquire and release a mutex lock automatically within a scope.
* `std::unique_lock`: Provides more flexibility than `std::lock_guard` by allowing the lock to be acquired and released manually.

Example:
```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mutexObj1, mutexObj2; // Mutexes for synchronization

// Function to be executed by the thread
void threadFunction()
{
    std::lock(mutexObj1, mutexObj2); // Lock multiple mutexes simultaneously

    // Critical section protected by both mutexes
    std::cout << "Thread function executing\n";

    // Unlock the mutexes
    mutexObj1.unlock();
    mutexObj2.unlock();
}

int main()
{
    std::thread threadObj(threadFunction);

    // Main thread execution

    {
        std::lock_guard<std::mutex> lock1(mutexObj1); // Lock mutex1 using std::lock_guard
        std::lock_guard<std::mutex> lock2(mutexObj2); // Lock mutex2 using std::lock_guard

        // Critical section protected by both mutexes
    }

    // Locks released when lock1 and lock2 go out of scope

    threadObj.join();

    return 0;
}
```
In this example, we have two mutexes `mutexObj1` and `mutexObj2`. Inside the `threadFunction`, we use `std::lock` to lock both mutexes simultaneously, ensuring that the critical section is executed without deadlock.

In the `main` function, we use a scope `{ }` to clearly indicate the critical section protected by the locks. Within this scope, we create `std::lock_guard` objects `lock1` and `lock2` to lock `mutexObj1` and `mutexObj2`, respectively.

The `std::lock_guard` objects automatically acquire the locks when they are created, and they automatically release the locks when they go out of scope. By placing the critical section within the scope, the locks are released automatically at the end of the scope, ensuring that other threads can access the protected resources.

This ensures the safety of the critical section and prevents potential issues like forgetting to release the locks manually, leading to deadlock or resource contention.

Finally, the `threadObj` is joined to wait for the thread execution to complete before the program exits.

By using the appropriate scoping and `std::lock_guard`, we ensure that the locks are released automatically when they go out of scope, providing a convenient and safe mechanism for releasing locks and avoiding resource contention in multi-threaded environments.

### Deadlock, Livelock, and Starvation: Causes and Prevention

Deadlock, livelock, and starvation are common problems in concurrent programming:

* Deadlock occurs when two or more threads are blocked, waiting for each other to release resources.
* Livelock occurs when threads are not blocked but still cannot make progress due to repeated interactions.
* Starvation occurs when a thread is constantly denied access to resources it requires, causing it to be unable to progress.

Preventing these issues requires careful synchronization and resource management.

Providing an example is not applicable as it requires a detailed scenario to demonstrate the problems and prevention techniques.

## Condition Variables (C++11 onwards)
### Overview of `std::condition_variable`
`std::condition_variable` provides a synchronization primitive for thread coordination and communication. It allows threads to wait for a certain condition to become true and be notified by another thread when the condition is met.

Example:
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mutexObj;
std::condition_variable condVar;
bool condition = false;

// Function to be executed by the thread waiting for the condition
void waitForCondition()
{
    std::unique_lock<std::mutex> lock(mutexObj);

    // Wait until the condition is met
    condVar.wait(lock, [] { return condition; });

    // Condition is met, continue execution
    std::cout << "Condition is met, continuing execution\n";
}

// Function to be executed by the thread notifying the condition
void notifyCondition()
{
    std::this_thread::sleep_for(std::chrono::seconds(2));

    {
        std::lock_guard<std::mutex> lock(mutexObj);

        // Update the condition
        condition = true;
    }

    // Notify the waiting thread
    condVar.notify_one();
}

int main()
{
    std::thread thread1(waitForCondition);
    std::thread thread2(notifyCondition);

    thread1.join();
    thread2.join();

    return 0;
}
```
In this example, we have a condition variable named `condVar` along with a mutex `mutexObj`. We also have a boolean variable `condition` that represents the condition we are waiting for.

The `waitForCondition` function is executed by a thread that waits for the condition to become true. It uses a `std::unique_lock` to lock the mutex and then calls `condVar.wait()` to wait for the condition to be met. The lambda function `[] { return condition; }` is used as a predicate to check the condition.

The `notifyCondition` function is executed by another thread that updates the condition after a delay of 2 seconds. It uses a `std::lock_guard` to lock the mutex, updates the condition, and then calls `condVar.notify_one()` to notify the waiting thread.

The `main` function creates two threads: one for waiting on the condition (`thread1`) and another for notifying the condition (`thread2`). After both threads have finished their execution, the program exits.

When you run this code, you will see the following output:
```cpp
Condition is met, continuing execution
```
The waiting thread (`thread1`) waits until the condition becomes true and is notified by the notifying thread (`thread2`). Once the condition is met, the waiting thread continues its execution.

### Use Cases for Condition Variables (Signaling Between Threads, Producer-Consumer Problem)
Condition variables are useful for scenarios where threads need to communicate and synchronize their actions based on certain conditions.

#### Signaling Between Threads
In this scenario, one thread waits for a condition to be met while another thread performs some actions and signals the waiting thread when the condition is met.

Example:
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mutexObj;
std::condition_variable condVar;
bool isReady = false;

// Function to be executed by the waiting thread
void waitForSignal()
{
    std::unique_lock<std::mutex> lock(mutexObj);

    // Wait until the signal is received
    condVar.wait(lock, [] { return is
    std::unique_lock<std::mutex> lock(mutexObj);

    // Wait until the signal is received
    condVar.wait(lock, [] { return isReady; });

    // Signal received, continue execution
    std::cout << "Signal received, continuing execution\n";
}

// Function to be executed by the signaling thread
void sendSignal()
{
    std::this_thread::sleep_for(std::chrono::seconds(2));

    {
        std::lock_guard<std::mutex> lock(mutexObj);

        // Set the condition to true
        isReady = true;
    }

    // Notify the waiting thread
    condVar.notify_one();
}

int main()
{
    std::thread thread1(waitForSignal);
    std::thread thread2(sendSignal);

    thread1.join();
    thread2.join();

    return 0;
}
```
In this example, we have a condition variable named `condVar` along with a mutex `mutexObj`. We also have a boolean variable `isReady` that represents the condition we are waiting for.

The `waitForSignal` function is executed by a thread that waits for the signal to be received. It uses a `std::unique_lock` to lock the mutex and then calls `condVar.wait()` to wait for the condition to be met. The lambda function `[] { return isReady; }` is used as a predicate to check the condition.

The `sendSignal` function is executed by another thread that sends the signal after a delay of 2 seconds. It uses a `std::lock_guard` to lock the mutex, updates the condition, and then calls `condVar.notify_one()` to notify the waiting thread.

The `main` function creates two threads: one for waiting for the signal (`thread1`) and another for sending the signal (`thread2`). After both threads have finished their execution, the program exits.

When you run this code, you will see the following output:
```cpp
Signal received, continuing execution
```
The waiting thread (`thread1`) waits until the signal is received from the signaling thread (`thread2`). Once the signal is received, the waiting thread continues its execution.

#### Producer-Consumer Problem
In this scenario, one or more producer threads generate data, and one or more consumer threads consume the data. Condition variables can be used to signal the availability of data to consumers or the availability of space for producers.

Example:
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <queue>

std::mutex mutexObj;
std::condition_variable condVar;
std::queue<int> dataQueue;

// Function to be executed by the producer thread
void produceData()
{
    for (int i = 1; i <= 5; ++i) {
        std::this_thread::sleep_for(std::chrono::seconds(1));

        {
            std::lock_guard<std::mutex> lock(mutexObj);

            // Produce data and add it to the queue
            dataQueue.push(i);
            std::cout << "Produced data: " << i << std::endl;
        }

        // Notify the consumer thread
        condVar.notify_one();
    }
}

// Function to be executed by the consumer thread
void consumeData()
{
    while (true) {
        std::unique_lock<std::mutex> lock(mutexObj);

        // Wait until data is available
        condVar.wait(lock, [] { return !dataQueue.empty(); });

        // Consume the data from the queue
        int data = dataQueue.front();
        dataQueue.pop();
        std::cout << "Consumed data: " << data << std::endl;

        lock.unlock();

        // Check if all data is consumed
        if (data == 5) {
            break;
        }
    }
}

int main()
{
    std::thread producerThread(produceData);
    std::thread consumerThread(consumeData);

    producerThread.join();
    consumerThread.join();

    return 0;
}
```
In this example, we have a condition variable named `condVar` along with a mutex `mutexObj`. We also have a queue `dataQueue` to store the produced data.

The `produceData` function is executed by a producer thread that generates data and adds it to the data queue. It produces data from 1 to 5 and adds it to the queue with a delay of 1 second between each production. After producing each data item, it calls `condVar.notify_one()` to notify the consumer thread.

The `consumeData` function is executed by a consumer thread that consumes the data from the queue. It waits until data is available in the queue using `condVar.wait()` and the predicate `!dataQueue.empty()`. Once data is available, it consumes the data item from the front of the queue, prints it, and checks if it has consumed all the data. If the last data item (5) is consumed, the loop breaks and the consumer thread exits.

The `main` function creates two threads: one for producing data (`producerThread`) and another for consuming data (`consumerThread`). After both threads have finished their execution, the program exits.

When you run this code, you will see the following output:
```cpp
Produced data: 1
Consumed data: 1
Produced data: 2
Consumed data: 2
Produced data: 3
Consumed data: 3
Produced data: 4
Consumed data: 4
Produced data: 5
Consumed data: 5
```
The producer thread produces data from 1 to 5 and adds it to the queue. The consumer thread waits until data is available in the queue, consumes it, and prints the consumed data. This process continues until all the data items are produced and consumed.

Condition variables are powerful synchronization primitives that allow threads to coordinate and communicate efficiently. They are commonly used for scenarios such as signaling between threads and solving producer-consumer problems in multi-threaded environments.