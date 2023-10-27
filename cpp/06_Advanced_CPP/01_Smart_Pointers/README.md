## Introduction to Smart Pointers
In C++, pointers are used to manage dynamic memory allocation. While using raw pointers, the programmer must manually allocate and deallocate memory, which can lead to issues such as memory leaks and dangling pointers. To overcome these issues, C++11 introduced smart pointers. Smart pointers are objects that behave like pointers, but they also provide additional features such as automatic memory management and exception safety.

### Importance of smart pointers
Smart pointers are important for several reasons:

* Memory management: Smart pointers automatically allocate and deallocate memory, which eliminates the risk of memory leaks and dangling pointers.
* Exception safety: Smart pointers ensure that resources are properly released in the event of an exception, which improves the reliability of the code.
* Resource ownership: Smart pointers help to enforce ownership semantics, which makes it clear which objects are responsible for managing a particular resource.

### Comparison of Smart Pointers with Raw Pointers
Smart pointers are similar to raw pointers, but they have some key differences:
* Smart pointers have ownership semantics, while raw pointers do not.
* Smart pointers automatically deallocate memory, while raw pointers do not.
* Smart pointers support exception safety, while raw pointers do not.

Here are the topics you will learn:

* [Unique Pointers](./01_unique_ptr.html)
* [Shared Pointers](./02_shared_ptr.html)
* [Weak Pointers](./03_weak_ptr.html)
* [Smart Pointers in Practice](./04_SPs_Practice.html)
* [Best Practices](./05_Best_Practices.html)