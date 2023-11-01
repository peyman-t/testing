## Advanced Socket Options
Advanced socket options provide additional control and customization over socket behavior in network programming. This section covers setting socket options, non-blocking sockets, I/O multiplexing, and socket timeouts.

### Understanding and Setting Socket Options
Socket options allow developers to configure various parameters related to socket behavior, such as reusing addresses, keeping connections alive, and managing linger time. These options enhance the flexibility and performance of network applications.

Commonly Used Socket Options:
* `SO_REUSEADDR`: Allows reusing the local address immediately after the socket is closed. This option is useful when binding to a recently used address.
* `SO_KEEPALIVE`: Enables sending periodic keep-alive messages to detect if a connection is still alive.
* `SO_LINGER`: Controls the behavior when closing a socket. It specifies whether the socket should linger (wait) for pending data to be sent or immediately close the connection.

### `setsockopt()` Function:

The `setsockopt()` function is used to set the value of a specific socket option. It allows you to configure various behaviors of the socket, such as enabling/disabling features or setting timeouts.

#### Syntax:
```cpp
int setsockopt(int sockfd, int level, int optname, const void *optval, socklen_t optlen);
```

#### Parameters:

1. **sockfd**: This is the socket descriptor on which the option is to be set. In your example, it's `serverSocket`.

2. **level**: This specifies the protocol level at which the option resides. For generic socket-level options, `SOL_SOCKET` is used. Other levels, such as `IPPROTO_TCP` or `IPPROTO_IP`, can be used for protocol-specific options.

3. **optname**: This is the specific option to be set. In your example, you've used `SO_REUSEADDR`, `SO_KEEPALIVE`, and `SO_LINGER`.

4. **optval**: A pointer to the value for the option to be set. This could be a simple integer or a more complex structure, depending on the option.

5. **optlen**: The size of the option value. This is typically `sizeof(optval)`.

#### Return Value:
The function returns 0 on success and -1 on failure. In case of failure, `errno` is set to indicate the error.


### Non-blocking Sockets and I/O Multiplexing
Non-blocking sockets allow performing other tasks while waiting for network operations. I/O multiplexing mechanisms, such as `select()`, `poll()`, and `epoll()`, enable efficient handling of multiple sockets concurrently.

### Socket Timeouts
Socket timeouts define the maximum time to wait for a specific operation to complete. They prevent network operations from blocking indefinitely, providing better control and responsiveness in network applications.

Example: Setting Socket Options in C++
```cpp
#include <iostream>
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>

int main() {
    int serverSocket = socket(AF_INET, SOCK_STREAM, 0);
    if (serverSocket < 0) {
        std::cerr << "Socket creation error\n";
        return 1;
    }

    // Sets SO_REUSEADDR option
    int reuseAddr = 1;
    if (setsockopt(serverSocket, SOL_SOCKET, SO_REUSEADDR, &reuseAddr, sizeof(reuseAddr)) < 0) {
        std::cerr << "Failed to set SO_REUSEADDR option\n";
        return 1;
    }

    // Sets SO_KEEPALIVE option
    int keepAlive = 1;
    if (setsockopt(serverSocket, SOL_SOCKET, SO_KEEPALIVE, &keepAlive, sizeof(keepAlive)) < 0) {
        std::cerr << "Failed to set SO_KEEPALIVE option\n";
        return 1;
    }

    // Sets SO_LINGER option
    struct linger lingerOption{};
    lingerOption.l_onoff = 1;
    lingerOption.l_linger = 5;  // Wait for 5 seconds before closing the connection
    if (setsockopt(serverSocket, SOL_SOCKET, SO_LINGER, &lingerOption, sizeof(lingerOption)) < 0) {
        std::cerr << "Failed to set SO_LINGER option\n";
        return 1;
    }

    // Further configuration and usage of the socket
    // ...

    close(serverSocket);

    return 0;
}
```
In this example, socket options are set on a TCP server socket. The `setsockopt()` function is used to configure the socket options. Three commonly used options are demonstrated: `SO_REUSEADDR` allows reusing the local address, `SO_KEEPALIVE` enables keep-alive messages, and `SO_LINGER` controls the linger behavior when closing the socket.

Example: Using Non-blocking Sockets in C++
```cpp
#include <iostream>
#include <sys/socket.h>
#include <netinet/in.h>
#include <fcntl.h>

int main() {
    int clientSocket = socket(AF_INET, SOCK_STREAM, 0);
    if (clientSocket < 0) {
        std::cerr << "Socket creation error\n";
        return 1;
    }

    // Sets the socket to non-blocking mode
    int flags = fcntl(clientSocket, F_GETFL, 0);
    if (flags < 0) {
        std::cerr << "Failed to get socket flags\n";
        return 1;
    }
    if (fcntl(clientSocket, F_SETFL, flags | O_NONBLOCK) < 0) {
        std::cerr << "Failed to set socket to non-blocking mode\n";
        return 1;
    }

    // Further configuration and usage of the socket
    // ...

    close(clientSocket);

    return 0;
}
```
In this example, a client socket is created, and then the `fcntl()` function is used to retrieve the socket's current flags. The `O_NONBLOCK` flag is added to the existing flags using the bitwise OR operator to set the socket to non-blocking mode.

Example: Setting Socket Timeout in C++
```cpp
#include <iostream>
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>

int main() {
    int clientSocket = socket(AF_INET, SOCK_STREAM, 0);
    if (clientSocket < 0) {
        std::cerr << "Socket creation error\n";
        return 1;
    }

    struct timeval timeout{};
    timeout.tv_sec = 5;  // Timeout after 5 seconds
    timeout.tv_usec = 0;

    if (setsockopt(clientSocket, SOL_SOCKET, SO_RCVTIMEO, &timeout, sizeof(timeout)) < 0) {
        std::cerr << "Failed to set receive timeout\n";
        return 1;
    }

    // Further configuration and usage of the socket
    // ...

    close(clientSocket);

    return 0;
}
```
In this example, a client socket is created, and the `setsockopt()` function is employed to configure its behavior. The `SOL_SOCKET` level is specified, indicating that the option being set is a socket-level option. The receive timeout option (`SO_RCVTIMEO`) is then set using this level. The timeout duration is defined as 5 seconds with the help of the `timeval` structure. As a result, if the socket doesn't receive any data within this 5-second window, it will return an error.

Advanced socket options provide fine-grained control over socket behavior, allowing developers to optimize network applications according to their specific requirements. By understanding and utilizing these options, developers can enhance the performance, reliability, and responsiveness of their network applications.