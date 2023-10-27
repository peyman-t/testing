## Chat Application

### Introduction

**Learning objectives** 
The assignment tests whether you can:

1. Understand the core concepts of multithreading in C++, including thread creation, synchronization, and mutexes.
2. Learn and implement network programming techniques in C++ using sockets and network communication.
3. Develop the ability to design and build concurrent and networked applications in C++.
4. Apply thread synchronization techniques to avoid race conditions and ensure the correct execution of concurrent programs.
5. Gain practical experience in handling network communication, including establishing connections, sending, and receiving data.

### Case/brief/scenario

Develop a concurrent and networked chat application in C++ that allows multiple clients to connect to a chat server and exchange messages in real-time. Implement multithreading for handling multiple client connections and use sockets for network communication between the server and clients.

### Requirements:

1. Chat Server:
    1. Implement a chat server using C++ network programming techniques, such as sockets, to listen for incoming client connections.
    2. Create a multithreaded server that can handle multiple client connections simultaneously.
    3. Implement proper thread synchronization techniques, such as mutexes, to avoid race conditions and ensure correct message handling.
    4. Design the server to broadcast incoming messages from clients to all connected clients.
    5. Implement error handling for network communication and multithreading issues.
2. Chat Client:
    1. Create a chat client using C++ network programming techniques, such as sockets, to connect to the chat server.
    2. Implement a multithreaded client to handle simultaneous sending and receiving of messages.
    3. Design a user-friendly command-line interface for users to input messages and view the received messages in real-time.
    4. Implement error handling for network communication and multithreading issues.

### Deliverable
A link to the git repository containing the program.