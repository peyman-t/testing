
## Classes Relationships
In C++, classes and objects can have different types of relationships with each other. These relationships can be categorized into three main types: composition, aggregation, and association. Additionally, inheritance is another type of class relationship that will be discussed in the next section.

### Composition
Composition is a strong "has-a" relationship, where a class object is made up of one or more objects of other classes. The contained objects cannot exist without the containing object. For example, consider a Car class that contains an Engine object. The Engine object cannot exist without the Car object, and if the Car object is destroyed, the Engine object is destroyed as well.

Here is an example of a class using composition:
```cpp
#include <iostream>

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

It is important to note that in Composition, the part (`Engine`) has no knowledge of the whole (`Car`) and therefore cannot directly send messages to the Car object. The interaction between the Engine and Car objects occurs through the Car's member functions that utilize the Engine object's functionality.

### Aggregation 
Aggregation is a weak "has-a" relationship, where a class object is made up of one or more objects of other classes, but the contained objects can exist independently. For example, consider a University class that has many Student objects. The Student objects can exist even if the `University` object is destroyed.

Here is an example of a class using aggregation:
```cpp
#include <iostream>

class Student {
private:
    std::string name;
    int age;

public:
    Student(const std::string& studentName, int studentAge)
        : name(studentName), age(studentAge) {}

    const std::string& getName() const {
        return name;
    }

    int getAge() const {
        return age;
    }
};

class University {
private:
    Student* students[100];
    int numStudents = 0;

public:
    void addStudent(Student* student) {
        if (numStudents >= 100) {
            std::cout << "Error: University has reached maximum capacity of 100 students." << std::endl;
            return;
        }
        students[numStudents] = student;
        numStudents++;
    }
    
    int getNumStudents() {return numStudents;}
    
    Student* getStudent(int index) {return students[index];}
};

int main() {
    Student s1{ "Alice", 20 };
    Student s2{ "Bob", 22 };

    University uni;
    uni.addStudent(&s1);
    uni.addStudent(&s2);

    // Example usage to access student information through the University
    std::cout << "University has " << uni.getNumStudents() << " students:" << std::endl;
    for (int i = 0; i < uni.getNumStudents(); i++) {
        const Student* student = uni.getStudent(i);
        std::cout << "Name: " << student->getName() << ", Age: " << student->getAge() << std::endl;
    }

    return 0;
}
```
In this example, the `University` class has a collection of `Student` objects. The `Student` objects can exist independently of the `University` object, and their lifetime is not tied to the `University` object's lifetime. The `University` object has access to the Student objects through its own member functions.

It is worth noting that aggregation is also unidirectional, meaning that the member class has no knowledge of the containing class and does not maintain a reference to it. The containing class may have multiple instances of the member class, and the member objects can exist independently outside the scope of the containing class.

### Association
Association is a relationship between two or more objects that allows them to communicate with each other to perform some functionality. In C++, association is represented using pointers or references in a class to establish a relationship with other classes. The associated objects can exist independently, meaning the lifetime of one object doesn't affect the lifetime of the other.

Here is an example of two classes using association: Let's consider a simplified scenario where each `Person` can be married to one other `Person`. In this case, each `Person` object needs a pointer to another `Person` object to represent their spouse. Here's an example:

```cpp
#include <iostream>
#include <string>

class Person {
public:
    std::string name;
    Person* spouse;  // Pointer to a Person object representing the spouse

    Person(std::string n) : name(n), spouse(nullptr) {}

    void marry(Person* p) {
        spouse = p;  // This person marries p
        p->spouse = this;  // p marries this person
    }

    void display() {
        if (spouse) {
            std::cout << name << " is married to " << spouse->name << std::endl;
        } else {
            std::cout << name << " is not married." << std::endl;
        }
    }
};

int main() {
    Person p1("Alice"), p2("Bob");

    p1.marry(&p2);

    p1.display();  // Outputs: Alice is married to Bob
    p2.display();  // Outputs: Bob is married to Alice

    return 0;
}
```

In this example, the `Person` class has a `spouse` pointer that points to another `Person` object. When two people get married, they each set their `spouse` pointer to point to the other person. The `display` function then prints who each person is married to. In the `main` function, we create two `Person` objects `p1` and `p2`, representing Alice and Bob, and then we make them marry each other. The `display` function then confirms that Alice is married to Bob and Bob is married to Alice.

Note that association and aggregation are two types of relationships that can exist between classes in object-oriented programming. Here's how they differ:

**Association:** This is a general binary relationship that describes an activity between two classes. For example, a `Teacher` teaches a `Student`. Here, both can exist independently. If the `Teacher` goes away, the `Student` can still exist, and vice versa. The association relationship can be bi-directional, with each class holding a reference to the other, or uni-directional, with one class holding a reference to the other but not vice versa.

**Aggregation:** This is a special form of association, which represents an "owns" relationship, or a whole/part relationship. For example, a `Department` can aggregate several `Employee` objects. If the `Department` is destroyed, the `Employee` objects can continue to exist; they aren't part of the `Department`, but the `Department` is composed of `Employee` objects. In other words, aggregation implies a relationship where the child can exist independently of the parent.

The key difference between association and aggregation is the dependency between the objects in the relationship. In an association, the objects are loosely coupled and can exist independently. In an aggregation, while the objects can still exist independently, there is a clear ownership relationship where one object (the parent or whole) is composed of one or more other objects (the children or parts).