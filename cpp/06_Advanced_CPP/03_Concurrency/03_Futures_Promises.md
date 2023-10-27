## Futures and Promises (C++11 onwards)
### Overview of `std::future` and `std::promise`
`std::future` and `std::promise` are components of the futures and promises mechanism in C++. They provide a way to asynchronously retrieve values from a separate thread and perform asynchronous computations.

Example:
```cpp
#include <iostream>
#include <thread>
#include <future>

// Function to be executed by the thread and return a value
int addNumbers(int a, int b)
{
    return a + b;
}

int main()
{
    // Create a promise and get the associated future
    std::promise<int> promiseObj;
    std::future<int> futureObj = promiseObj.get_future();

    // Create a thread to perform the computation
    std::thread threadObj([&promiseObj] {
        int result = addNumbers(10, 20);

        // Set the value in the promise
        promiseObj.set_value(result);
    });

    // Wait for the future to receive the value
    int result = futureObj.get();

    std::cout << "Result: " << result << std::endl;

    threadObj.join();

    return 0;
}
```
In this example, we have a function `addNumbers` that takes two integers as parameters and returns their sum.

In the `main` function, we create a `std::promise` object named `promiseObj` and obtain its associated `std::future` using `get_future()`. This establishes a communication channel between the main thread and the thread that will perform the computation.

We create a separate thread using a lambda function. Inside the lambda function, we perform the computation by calling `addNumbers` and store the result in the `result` variable. We then set the value of the promise using `set_value(result)`.

Back in the main thread, we call `get()` on the `futureObj` to retrieve the value computed by the separate thread. The `get()` call blocks the main thread until the future receives the value from the promise.

Once we have the result, we print it, join the separate thread, and exit the program.

When you run this code, you will see the following output:
```cpp
Result: 30
```
The separate thread performs the computation of adding numbers 10 and 20. The result is then passed through the promise to the future, and the main thread retrieves and prints the value.

### Use Cases for Futures and Promises (Returning Data from Threads, Asynchronous Computations)

Futures and promises are commonly used in scenarios where you want to retrieve values from separate threads or perform asynchronous computations.

#### Returning Data from Threads
In this scenario, a thread performs some computation and returns a value that can be retrieved by the calling thread using a future.

Example:
```cpp
#include <iostream>
#include <thread>
#include <future>

// Function to be executed by the thread and return a value
int multiplyNumbers(int a, int b)
{
    return a * b;
}

int main()
{
    // Create a promise and get the associated future
    std::promise<int> promiseObj;
    std::future<int> futureObj = promiseObj.get_future();

    // Create a thread to perform the computation
    std::thread threadObj([&promiseObj] {
        int result = multiplyNumbers(5, 7);

        // Set the value in the promise
        promiseObj.set_value(result);
    });

    // Wait for the future to receive the value
    int result = futureObj.get();

    std::cout << "Result: " << result << std::endl;

    threadObj.join();

    return 0;
}
```
In this example, we have a function `multiplyNumbers` that takes two integers as parameters and returns their product.

Similar to the previous example, we create a `std::promise` object named `promiseObj` and obtain its associated `std::future` using `get_future()`.

Inside the lambda function, we perform the computation by calling `multiplyNumbers` and store the result in the result variable. We then set the value of the promise using `set_value(result)`.

Back in the main thread, we call `get()` on the `futureObj` to retrieve the computed value. The `get()` call blocks the main thread until the future receives the value from the promise.

Once we have the result, we print it, join the separate thread, and exit the program.

When you run this code, you will see the following output:
```cpp
Result: 35
```
The separate thread performs the computation of multiplying numbers 5 and 7. The result is then passed through the promise to the future, and the main thread retrieves and prints the value.

#### Asynchronous Computations
In this scenario, you can perform multiple computations concurrently and retrieve their results asynchronously using futures.

Example:
```cpp
#include <iostream>
#include <future>

// Function to be executed asynchronously and return a value
int square(int x)
{
    return x * x;
}

int main()
{
    // Perform computations asynchronously
    std::future<int> future1 = std::async(square, 5);
    std::future<int> future2 = std::async(square, 7);
    std::future<int> future3 = std::async(square, 9);

    // Retrieve the results asynchronously
    int result1 = future1.get();
    int result2 = future2.get();
    int result3 = future3.get();

    std::cout << "Result 1: " << result1 << std::endl;
    std::cout << "Result 2: " << result2 << std::endl;
    std::cout << "Result 3: " << result3 << std::endl;

    return 0;
}
```
In this example, we have a function `square` that takes an integer as a parameter and returns its square.

We use `std::async` to perform the computations asynchronously. Each call to `std::async` creates a separate task that will execute the `square` function with the specified argument.

We obtain three futures `future1`, `future2`, and `future3` that represent the results of the computations.

We then call `get()` on each future to retrieve the results synchronously. The `get()` calls block until the corresponding futures receive the computed values.

Finally, we print the results of each computation.

When you run this code, you will see the following output:
```cpp
Result 1: 25
Result 2: 49
Result 3: 81
```
The computations for squaring numbers 5, 7, and 9 are performed asynchronously using `std::async`. The results are retrieved using `get()` on the corresponding futures, and the values are printed.

Futures and promises provide a convenient mechanism for returning values from threads and performing asynchronous computations. They enable you to retrieve results from separate threads without explicitly managing thread synchronization.