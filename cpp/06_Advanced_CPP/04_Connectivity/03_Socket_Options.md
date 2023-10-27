## Advanced Socket Options
Advanced socket options provide additional control and customization over socket behavior in network programming. This section covers setting socket options, non-blocking sockets, I/O multiplexing, and socket timeouts.

### Understanding and Setting Socket Options
Socket options allow developers to configure various parameters related to socket behavior, such as reusing addresses, keeping connections alive, and managing linger time. These options enhance the flexibility and performance of network applications.

Commonly Used Socket Options:
* `SO_REUSEADDR`: Allows reusing the local address immediately after the socket is closed. This option is useful when binding to a recently used address.
* `SO_KEEPALIVE`: Enables sending periodic keep-alive messages to detect if a connection is still alive.
* `SO_LINGER`: Controls the behavior when closing a socket. It specifies whether the socket should linger (wait) for pending data to be sent or immediately close the connection.

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

    // Set SO_REUSEADDR option
    int reuseAddr = 1;
    if (setsockopt(serverSocket, SOL_SOCKET, SO_REUSEADDR, &reuseAddr, sizeof(reuseAddr)) < 0) {
        std::cerr << "Failed to set SO_REUSEADDR option\n";
        return 1;
    }

    // Set SO_KEEPALIVE option
    int keepAlive = 1;
    if (setsockopt(serverSocket, SOL_SOCKET, SO_KEEPALIVE, &keepAlive, sizeof(keepAlive)) < 0) {
        std::cerr << "Failed to set SO_KEEPALIVE option\n";
        return 1;
    }

    // Set SO_LINGER option
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
        std::cerr << "Socket
        creation error\n";
        return 1;
    }

    // Set the socket to non-blocking mode
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
In this example, a client socket is created, and the `setsockopt()` function is used to set the receive timeout option (`SO_RCVTIMEO`). The timeout is set to 5 seconds using the timeval structure. This ensures that if no data is received within the specified timeout period, the socket will return an error.

Advanced socket options provide fine-grained control over socket behavior, allowing developers to optimize network applications according to their specific requirements. By understanding and utilizing these options, developers can enhance the performance, reliability, and responsiveness of their network applications.