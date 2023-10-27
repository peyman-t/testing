
## Classes Relationships
In C++, classes and objects can have different types of relationships with each other. These relationships can be categorized into three main types: composition, aggregation, and association.

### Composition
Composition is a strong "has-a" relationship, where a class object is made up of one or more objects of other classes. The contained objects cannot exist without the containing object. For example, consider a Car class that contains an Engine object. The Engine object cannot exist without the Car object, and if the Car object is destroyed, the Engine object is destroyed as well.

Here is an example of a class using composition:
```cpp
class Engine {
public:
    void start() { std::cout << "Engine started." << std::endl; }
    void stop() { std::cout << "Engine stopped." << std::endl; }
};

class Car {
private:
    Engine engine;

public:
    void startCar() { engine.start(); }
    void stopCar() { engine.stop(); }
};

int main() {
    Car car;
    car.startCar();
    car.stopCar();

    return 0;
}
```
In this example, the Car class is composed of an Engine object. The Car object cannot exist without the Engine object, and the Engine object's lifetime is tied to the Car object's lifetime. The Car object has access to the Engine object's member functions through its own member functions.

### Aggregation 
Aggregation is a weak "has-a" relationship, where a class object is made up of one or more objects of other classes, but the contained objects can exist independently. For example, consider a University class that has many Student objects. The Student objects can exist even if the `University` object is destroyed.

Here is an example of a class using aggregation:
```cpp
class Student {
public:
    std::string name;
    int age;
};

class University {
public:
    Student students[100];
    int numStudents = 0;

    void addStudent(Student student) {
        if (numStudents >= 100) {
            std::cout << "Error: University has reached maximum capacity of 100 students." << std::endl;
            return;
        }
        students[numStudents] = student;
        numStudents++;
    }
};

int main() {
    Student s1 { "Alice", 20 };
    Student s2 { "Bob", 22 };

    University uni;
    uni.addStudent(s1);
    uni.addStudent(s2);

    return 0;
}
```
In this example, the `University` class has a collection of `Student` objects. The `Student` objects can exist independently of the `University` object, and their lifetime is not tied to the `University` object's lifetime. The `University` object has access to the Student objects through its own member functions.

### Association
Association is a relationship between two or more classes, where one class object can use another class object. It is a "knows-a" relationship. For example, consider a Bank class and a Customer class. A Bank object can have multiple Customer objects associated with it. The Customer objects can exist independently of the Bank object, but they have a relationship with it.

Here is an example of two classes using association:
```cpp
class Bank {
public:
    std::string name;
    void deposit(int amount) { /* deposit implementation */ }
    void withdraw(int amount) { /* withdraw implementation */ }
};

class Customer {
public:
    std::string name;
    Bank* bank;

    Customer(std::string name, Bank* bank) : name(name), bank(bank) {}

    void deposit(int amount) { bank->deposit(amount); }
    void withdraw(int amount) { bank->withdraw(amount); }
};

int main() {
    Bank bank { "ABC Bank" };
    Customer c1 { "Alice", &bank };
    Customer c2 { "Bob", &bank };

    c1.deposit(100);
    c2.withdraw(50);

    return 0;
}
```
This example shows an association between the `Bank` and `Customer` classes. The `Customer` class has a pointer to a `Bank` object, which allows the customer to interact with the bank by depositing and withdrawing money. The `Bank` class, on the other hand, has no direct knowledge of its customers. The association between the two classes is unidirectional, meaning that the `Bank` class is not aware of the `Customer` class. This example demonstrates how objects can be associated with one another without being fully dependent on each other, providing flexibility and modularity in the design of software systems.