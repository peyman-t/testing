### Open/Closed Principle (OCP)
The Open/Closed Principle (OCP) is a software design principle that states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, we should be able to add new functionality to a software system without having to modify the existing code. This makes software more extensible and less prone to errors caused by modification of existing code.

One way to achieve this is by using inheritance and polymorphism. By defining an abstract base class that defines a set of functions that can be overridden in derived classes, we can provide a way to extend the functionality of the software without modifying the existing code. This way, the software can be easily extended by adding new derived classes that implement new functionality.

Let's consider a scenario where we have an `Employee` class with a `calculateBonus()` method. Initially, it only supports a flat bonus calculation. Later, we want to extend it to calculate bonuses differently for `Manager` and `Developer` roles. A violation of the Open/Closed Principle (OCP) would be if we modify the `Employee` class each time we add support for a new role.

Here's an example:

```cpp
class Employee {
public:
    enum Role {Manager, Developer};
    Role role;

    // Constructor
    Employee(Role r) : role(r) {}

    double calculateBonus(double salary) {
        if (role == Manager) {
            return salary * 0.1;  // 10% bonus for managers
        }
        else if (role == Developer) {
            return salary * 0.05;  // 5% bonus for developers
        }
        else {
            return 0.0;  // No bonus for other roles
        }
    }
};
```
In this example, the `calculateBonus()` method of the `Employee` class has to be modified each time a new role is added to the system. This violates the Open/Closed Principle because the `Employee` class is not closed for modification. A better approach would be to have a separate class for each role, each with its own implementation of the `calculateBonus()` method. This way, when a new role is added, we just need to add a new class without modifying the existing ones.

Now, consider a class hierarchy for different types of employees. We can define a base class `Employee` with a pure virtual function `calculateBonus()`. We can then define derived classes `Manager`, `HourlyEmployee`, and `SalaryEmployee`, each with their own implementation of the `calculateBonus()` function. If we want to add a new type of employee, say `CommissionedEmployee`, we can simply create a new derived class that implements its own `calculateBonus()` function without having to modify the existing code. Here is the code:
```cpp
class Employee {
public:
    virtual double calculateBonus() = 0; // Pure virtual function
};

class Manager : public Employee {
public:
    double calculateBonus() override {
        // implementation for manager bonus calculation
    }
};

class HourlyEmployee : public Employee {
public:
    double calculateBonus() override {
        // implementation for hourly employee bonus calculation
    }
};

class SalaryEmployee : public Employee {
public:
    double calculateBonus() override {
        // implementation for salary employee bonus calculation
    }
};

class CommissionedEmployee : public Employee {
public:
    double calculateBonus() override {
        // implementation for commissioned employee bonus calculation
    }
};
```
This is an example of the Open/Closed Principle (OCP) in action, as the code is open for extension (adding new employee types) but closed for modification (we don't need to modify the existing code to add new employee types).

Violating the OCP can have serious consequences, such as making the software more difficult to maintain, causing errors due to unintended side effects of modifying existing code, and making it more difficult to add new functionality to the software.