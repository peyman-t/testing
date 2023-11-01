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

#### Visualizing Race Conditions in Multithreading
The figure below is the depicted scenario of the two threads above, `Thread1` and `Thread2`, that are attempting to increment a shared variable `counter`. The textual representation demonstrates the unpredictable nature of concurrent execution:

1. `Thread1` starts and increments the `counter`.
2. Before `Thread1` can increment again, `Thread2` jumps in and increments the `counter`.
3. Both threads continue this pattern, but the exact order of their operations is not guaranteed.

The key takeaway is the question marks (`?`) in the shared variable column. These represent the uncertainty in the value of `counter` at any given time due to the concurrent increments. This unpredictability is the essence of a race condition. Without proper synchronization, the final value of `counter` can vary between different runs of the program, leading to unreliable and erroneous outcomes.

```lua
   Thread1          Shared Variable (counter)          Thread2
      |                     | 0                        |
      |                     |                          |
      |------ Increment --->|                          |
      |                     | 1                        |
      |                     |                          |
      |                     |                          |
      |                     |                          |
      |                     | 1                        |
      |                     |<----- Increment ---------|
      |                     | 2                        |
      |                     |                          |
      |                     |                          |
      |------ Increment --->|                          |
      |                     | ?                        |
      |                     |                          |
      |                     |                          |
      |                     | ?                        |
      |                     |<----- Increment ---------|
      |                     | ?                        |
      |                     |                          |
      |                     |                          |
      |------ Increment --->|                          |
      |                     | ?                        |
      |                     |                          |
```

### Understanding `std::mutex` for Mutual Exclusion in Multithreading
In the realm of multithreading, ensuring that shared resources are accessed in a controlled manner is crucial. This is where `std::mutex` comes into play. The term "mutex" stands for "mutual exclusion," and as the name suggests, it is a tool that ensures that only one thread can access a particular resource or section of code at any given moment.

When a thread wants to access a shared resource, it first tries to acquire the lock associated with the `std::mutex`. If the lock is available (i.e., not held by another thread), the thread acquires it and proceeds to access the resource. During this period, any other thread that attempts to acquire the same lock will be blocked and will have to wait.

This mechanism ensures that shared resources, such as global variables or shared data structures, are not accessed simultaneously by multiple threads, which could lead to unpredictable behavior or data corruption. Once the thread that holds the lock is done with the resource, it releases the lock, allowing other waiting threads to acquire it and access the resource in turn.

In essence, `std::mutex` acts as a gatekeeper, ensuring orderly and safe access to shared resources in a multithreaded environment.

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


### Locking Strategies: Understanding `std::lock`, `std::lock_guard`, and `std::unique_lock`
In multithreaded programming, ensuring that shared resources are accessed safely is paramount. This is achieved using synchronization primitives that help in locking and unlocking mutexes. Among these primitives, `std::lock`, `std::lock_guard`, and `std::unique_lock` stand out for their specific functionalities:

1. **`std::lock`**: This primitive is designed to handle situations where a thread needs to acquire multiple mutexes. The challenge here is to ensure that while one thread is trying to lock multiple mutexes, another thread doesn't lock some of them in a different order, leading to a deadlock. A deadlock occurs when two or more threads are unable to proceed with their tasks because each is waiting for the other to release a resource. By locking multiple mutexes simultaneously, `std::lock` ensures a deadlock-free manner of acquiring locks, preventing such scenarios.

2. **`std::lock_guard`**: Think of `std::lock_guard` as a safety mechanism that automatically manages the life cycle of a mutex lock. When you create a `std::lock_guard` object, it immediately acquires the associated mutex. Importantly, when the `std::lock_guard` object goes out of scope, it releases the mutex. This ensures that the mutex is always unlocked, even if an exception occurs, making resource management safer and more convenient.

3. **`std::unique_lock`**: While `std::lock_guard` is convenient, it doesn't offer much flexibility. Enter `std::unique_lock`, which provides a more versatile approach to mutex management. With `std::unique_lock`, you have the power to manually lock and unlock the mutex. This is particularly useful in scenarios where you need conditional locking or want to transfer lock ownership between threads.

**Understanding Deadlock**: 
To delve deeper into the concept of deadlock, imagine two threads, A and B. Thread A locks mutex1 and waits to lock mutex2, while thread B locks mutex2 and waits to lock mutex1. In this scenario, neither thread can proceed because each is waiting for the other to release a mutex. This standstill situation, where threads are stuck indefinitely, is termed a deadlock. It's a critical issue in multithreading, as it can halt the progress of an application. Using synchronization primitives like `std::lock` can help in avoiding such situations.

**Understanding Critical Section**:
A critical section refers to a segment of code where a thread accesses shared resources, such as variables, data structures, or external devices, that must not be simultaneously accessed by other threads. Given the shared nature of these resources, any simultaneous access or modification can lead to unpredictable results, data corruption, or other unintended behaviors. To ensure that only one thread accesses the shared resource at a time, the critical section is protected by synchronization mechanisms like mutexes. When a thread enters a critical section, it acquires the necessary lock, preventing other threads from entering the same section. Once its task is complete, the thread releases the lock, allowing other threads to access the critical section. Proper management of critical sections is vital in multithreaded programming to maintain data integrity and system stability.


Example:
```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mutexObj1, mutexObj2; // Mutexes for synchronization
int sharedResource = 0; // A shared resource

// Function to be executed by the thread
void threadFunction()
{
    std::unique_lock<std::mutex> lock1(mutexObj1); // Lock mutexObj1 using std::unique_lock
    std::this_thread::sleep_for(std::chrono::milliseconds(1)); // Simulate some processing
    std::unique_lock<std::mutex> lock2(mutexObj2); // Lock mutexObj2 using std::unique_lock

    // Critical section protected by both mutexes
    sharedResource += 1;
    std::cout << "Thread function incremented sharedResource to: " << sharedResource << "\n";
}

int main()
{
    std::thread threadObj(threadFunction);

    // Main thread execution
    {
        std::unique_lock<std::mutex> lock1(mutexObj1); // Lock mutex1 using std::unique_lock
        std::this_thread::sleep_for(std::chrono::milliseconds(2)); // Simulate some processing
        std::unique_lock<std::mutex> lock2(mutexObj2); // Lock mutex2 using std::unique_lock

        // Critical section protected by both mutexes
        sharedResource += 10;
        std::cout << "Main thread incremented sharedResource to: " << sharedResource << "\n";
    }

    // Locks released when lock1 and lock2 go out of scope

    threadObj.join();

    return 0;
}
```
In this example, two mutexes, `mutexObj1` and `mutexObj2`, are defined globally. These mutexes are used to protect a shared resource.

The function `threadFunction` represents the task that a separate thread will execute. Inside this function, both mutexes are locked simultaneously using `std::lock`, ensuring a deadlock-free acquisition. After acquiring the locks, a message is printed to the console. Once the critical section (the part where the shared resource would typically be accessed) is executed, both mutexes are unlocked.

In the `main` function, a new thread (`threadObj`) is created to execute the `threadFunction`. Meanwhile, the main thread locks both mutexes using `std::lock_guard`, which automatically acquires the lock upon creation and releases it when going out of scope. The critical section in the main function is represented by the scope of the `std::lock_guard` objects. After the main thread completes its critical section, the locks are automatically released when the `std::lock_guard` objects go out of scope.

Finally, `threadObj.join()` ensures that the main function waits for the separate thread to finish its execution before proceeding. This ensures that the program doesn't end prematurely, leaving the thread incomplete.


### Understanding Deadlock, Livelock, and Starvation

In the realm of concurrent programming, Deadlock, Livelock, and Starvation represent critical challenges that can hinder system performance and reliability:

* **Deadlock**: This situation arises when two or more threads find themselves in a standstill, each waiting indefinitely for the other to release a resource. It's akin to a traffic jam where cars are stuck because they're blocking each other's paths.

* **Livelock**: Unlike deadlock where threads are completely blocked, in a livelock, threads remain active but are caught in an endless loop of interactions that prevent them from making any meaningful progress. Imagine two people trying to pass each other in a hallway, but they keep moving in the same direction, blocking each other's way.

* **Starvation**: Here, a thread consistently finds itself at the back of the line, perpetually denied the resources it needs. This results in the thread being unable to move forward, much like a person in a queue who never reaches the front.

To navigate these challenges, detailed synchronization and accurate resource management are important. 

Certainly! Let's illustrate these problems using a simple example involving two threads and two resources.

#### Example: Dining Philosophers Problem

In a quiet room, two philosophers sit across from each other at a small round table. Engaged in deep thought, they occasionally pause their musings to eat from the bowls of spaghetti placed in front of them. However, there's a catch: there are only two forks on the table, one placed between each philosopher's bowl.

For a philosopher to eat, they must use both forks. The left fork is closer to one philosopher, while the right fork is closer to the other. This setup leads to a conundrum:

1. **Initial Scenario**: Both philosophers, lost in thought, might feel the pangs of hunger at the same moment. Instinctively, each reaches for the fork closest to them. The philosopher on the left grabs the left fork, and the one on the right grabs the right fork.

2. **The Deadlock**: Now, both philosophers need the remaining fork to start eating. However, neither is willing to put down their fork, and neither can access the other fork. They are at an impasse, waiting indefinitely for the other to release the fork they need. This is a classic deadlock scenario.

3. **The Livelock**: Suppose the philosophers, being courteous, decide that if they can't get the second fork within a few seconds, they'll put down the fork they have and wait a moment before trying again. Now, imagine both philosophers picking up a single fork, realizing the other fork is unavailable, and then simultaneously putting their forks down. They wait, then both try again at the same time, repeating the cycle. They're active, continuously trying to eat, but neither makes any progress. This repetitive dance is a livelock.

4. **Starvation**: Over time, it might happen that one philosopher, either by chance or strategy, manages to pick up both forks more frequently than the other. While this philosopher enjoys his spaghetti, the other waits. If this pattern continues, one philosopher might get to eat regularly, while the other rarely or never gets both forks at the same time. The latter philosopher is experiencing starvation, perpetually denied the chance to eat.

Here is the code:
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <chrono>

std::mutex fork1, fork2;

void philosopherA() {
    while (true) {
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // thinking
        fork1.lock(); // picks up left fork
        if (!fork2.try_lock()) { // tries to pick up right fork
            fork1.unlock(); // if right fork is not available, puts down left fork
            continue; // this can lead to livelock if both philosophers keep picking and dropping forks without eating
        }
        std::cout << "Philosopher A is eating\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // eating
        fork2.unlock();
        fork1.unlock();
    }
}

void philosopherB() {
    while (true) {
        std::this_thread::sleep_for(std::chrono::milliseconds(150)); // thinking
        fork2.lock(); // picks up right fork
        if (!fork1.try_lock()) { // tries to pick up left fork
            fork2.unlock(); // if left fork is not available, put down right fork
            continue; // potential for livelock
        }
        std::cout << "Philosopher B is eating\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(150)); // eating
        fork1.unlock();
        fork2.unlock();
    }
}

int main() {
    std::thread A(philosopherA);
    std::thread B(philosopherB);

    A.join();
    B.join();

    return 0;
}
```
The above problems can be addressed using the three suggested strategies:

1. **Introducing a Waiter Arbitrator**: 
   A waiter (or arbitrator) can be introduced to give permission to a philosopher to pick up the forks. A philosopher must ask the waiter before picking up the forks. The waiter ensures that only one philosopher can pick up both forks at a time.

2. **Ordering Resource Requests**: 
   Philosophers can always pick up the lower-numbered fork first. This ensures that only one philosopher can get both forks at a time, preventing deadlock.

3. **Adding Randomness to Request Intervals**: 
   Philosophers can wait for a random amount of time before trying to pick up the forks again. This reduces the chance of livelock as both philosophers are less likely to act in perfect synchrony.

Let's modify the code using the "Ordering Resource Requests" strategy:

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <chrono>

std::mutex fork1, fork2;

void philosopherA() {
    while (true) {
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // thinking

        fork1.lock(); // pick up lower-numbered fork first
        fork2.lock(); // then pick up the other fork

        // Critical section
        std::cout << "Philosopher A is eating\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // eating

        fork2.unlock();
        fork1.unlock();
    }
}

void philosopherB() {
    while (true) {
        std::this_thread::sleep_for(std::chrono::milliseconds(150)); // thinking

        fork1.lock(); // pick up lower-numbered fork first
        fork2.lock(); // then pick up the other fork

        // Critical section
        std::cout << "Philosopher B is eating\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(150)); // eating

        fork2.unlock();
        fork1.unlock();
    }
}

int main() {
    std::thread A(philosopherA);
    std::thread B(philosopherB);

    A.join();
    B.join();

    return 0;
}
```

By ensuring that both philosophers always try to pick up `fork1` before `fork2`, we eliminate the possibility of deadlock. Both philosophers cannot be in a situation where one holds `fork1` and the other holds `fork2` because the ordering prevents such a scenario.

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

    // Waits until the condition is met
    condVar.wait(lock, [] { return condition; });

    // Condition is met, continues execution
    std::cout << "Condition is met, continuing execution\n";
}

// Function to be executed by the thread notifying the condition
void notifyCondition()
{
    std::this_thread::sleep_for(std::chrono::seconds(2));

    {
        std::lock_guard<std::mutex> lock(mutexObj);

        // Updates the condition
        condition = true;
    }

    // Notifies the waiting thread
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

### Use Cases for Condition Variables (Signaling Between Threads, Producer-Consumer Problem)
Condition variables are useful for scenarios where threads need to communicate and synchronize their actions based on certain conditions.

#### Signaling Between Threads
In this scenario, one thread waits for a condition to be met while another thread performs some actions and signals the waiting thread when the condition is met. An example has been already demonstrated under the `std::condition_variable` section above.

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

            // Produces data and add it to the queue
            dataQueue.push(i);
            std::cout << "Produced data: " << i << std::endl;
        }

        // Notifies the consumer thread
        condVar.notify_one();
    }
}

// Function to be executed by the consumer thread
void consumeData()
{
    while (true) {
        std::unique_lock<std::mutex> lock(mutexObj);

        // Waits until data is available
        condVar.wait(lock, [] { return !dataQueue.empty(); });

        // Consumes the data from the queue
        int data = dataQueue.front();
        dataQueue.pop();
        std::cout << "Consumed data: " << data << std::endl;

        lock.unlock();

        // Checks if all data is consumed
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

Condition variables are powerful synchronization primitives that allow threads to coordinate and communicate efficiently. They are commonly used for scenarios such as signaling between threads and solving producer-consumer problems in multi-threaded environments.