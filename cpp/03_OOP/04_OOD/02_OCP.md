### Open/Closed Principle (OCP)
The Open/Closed Principle (OCP) is a software design principle that states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, we should be able to add new functionality to a software system without having to modify the existing code. This makes software more extensible and less prone to errors caused by modification of existing code.

One way to achieve this is by using inheritance and polymorphism. By defining an abstract base class that defines a set of functions that can be overridden in derived classes, we can provide a way to extend the functionality of the software without modifying the existing code. This way, the software can be easily extended by adding new derived classes that implement new functionality.

Assume an `Employee` class with a virtual function `calculatePay()` that calculates the pay for an employee and a virtual function `calculateBonus()` that calculates bonus for some types of employees: 
```cpp
class Employee {
public:
    virtual double calculatePay() = 0; // Pure virtual function
    virtual double calculateBonus() = 0; // New function added, violating OCP
};
```
By adding the function calculateBonus() to the `Employee` class, we are violating the OCP because any class that inherits from `Employee` will have to implement this function, even if it does not make sense for that particular type of employee. This violates the principle that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.

Now, consider a class hierarchy for different types of employees. We can define a base class `Employee` with a virtual function `calculatePay()` that calculates the pay for an employee. We can then define derived classes `Manager`, `HourlyEmployee`, and `SalaryEmployee`, each with their own implementation of the `calculatePay()` function. If we want to add a new type of employee, say `CommissionedEmployee`, we can simply create a new derived class that implements its own `calculatePay()` function without having to modify the existing code. Here is the code:
```cpp
class Employee {
public:
    virtual double calculatePay() = 0; // Pure virtual function
};

class Manager : public Employee {
public:
    double calculatePay() override {
        // implementation for manager pay calculation
    }
};

class HourlyEmployee : public Employee {
public:
    double calculatePay() override {
        // implementation for hourly employee pay calculation
    }
};

class SalaryEmployee : public Employee {
public:
    double calculatePay() override {
        // implementation for salary employee pay calculation
    }
};

class CommissionedEmployee : public Employee {
public:
    double calculatePay() override {
        // implementation for commissioned employee pay calculation
    }
};
```
This is an example of the Open/Closed Principle (OCP) in action, as the code is open for extension (adding new employee types) but closed for modification (we don't need to modify the existing code to add new employee types).

Violating the OCP can have serious consequences, such as making the software more difficult to maintain, causing errors due to unintended side effects of modifying existing code, and making it more difficult to add new functionality to the software.