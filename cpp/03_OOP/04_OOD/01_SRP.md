### Single Responsibility Principle (SRP)
The Single Responsibility Principle (SRP) is a principle of software design that states that a class or function should have only one responsibility, i.e., only one reason to change. In other words, a class or function should be responsible for doing one thing and doing it well.

Identifying responsibilities and separating concerns is the first step in applying SRP in C++. This means that we need to analyze our code and identify the various responsibilities that a class or function is currently handling. Once we have identified the various responsibilities, we need to separate them into different classes or functions, each with a single responsibility.

Here is an example of applying SRP in C++:

Suppose we have a class `CustomerData` that is responsible for both storing customer data and sending email notifications to customers. This violates SRP because the class has two distinct responsibilities: storing data and sending notifications. 
```cpp
class CustomerData {
public:
    void addCustomer(Customer customer) {
        // Add customer data to database
    }
    void updateCustomer(Customer customer) {
        // Update customer data in database
    }
    void deleteCustomer(Customer customer) {
        // Delete customer data from database
    }

    void sendNotification(Customer customer, string message) {
        // Send email notification to customer
    }
};
```
To apply SRP, we can separate these responsibilities into two classes: `CustomerData` and `CustomerNotifier`.
```cpp
class CustomerData {
public:
    void addCustomer(Customer customer) {
        // Add customer data to database
    }
    void updateCustomer(Customer customer) {
        // Update customer data in database
    }
    void deleteCustomer(Customer customer) {
        // Delete customer data from database
    }
};

class CustomerNotifier {
public:
    void sendNotification(Customer customer, string message) {
        // Send email notification to customer
    }
};
```
Consequences of violating SRP include code that is difficult to maintain, reuse, and test. When a class or function has multiple responsibilities, any change to one responsibility can potentially affect the other responsibilities, making it difficult to change the code without introducing bugs. Additionally, testing becomes more difficult because the different responsibilities may have different testing requirements. By applying SRP, we can create code that is easier to understand, maintain, and test.