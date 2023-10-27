## Base and Derived Class Relationships
In C++, when a class is derived from another class, it inherits all the members of the base class except for the constructors and destructors. The derived class can override the member functions inherited from the base class, and can also add new member functions or variables. The relationship between the base and derived classes can be characterized as an "is-a" relationship, where the derived class "is-a" specialization of the base class.

### Overriding Member Functions
When a derived class provides its own implementation for a member function that is already defined in the base class, it is called function overriding. The derived class overrides the implementation of the base class method by providing its own implementation that is more specific to the derived class. To override a function in the base class, the function in the derived class must have the same signature as the base class function. This means that the function name, return type, and argument list must be the same in both the base and derived class functions.

Example:
```cpp
class Shape {
public:
    virtual void draw() {
        std::cout << "Drawing a shape" << std::endl;
    }
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle" << std::endl;
    }
};

int main() {
    Shape* s = new Circle();
    s->draw(); // Output: "Drawing a circle"
    delete s;
    return 0;
}
```
In this example, we have a base class `Shape` with a virtual function `draw()`. The derived class `Circle` overrides the `draw()` function and provides its own implementation. In the `main()` function, we create an instance of the `Circle` class and assign it to a pointer of type `Shape*`. When we call the `draw()` function on the `Shape*` pointer, it calls the overridden version of the `draw()` function in the `Circle` class, resulting in the output "Drawing a circle". The `virtual` keyword in the base class function declaration specifies that it can be overridden by a derived class. The `override` keyword is used in the derived class function declaration to indicate that it is intended to override a virtual function from the base class. This keyword helps to prevent errors in the function signature, such as typos or parameter mismatches, that might otherwise result in a new function being created instead of overriding the intended base class function.

### Invoking Base Class Functions from Derived Classes
Sometimes it is necessary to call the base class implementation of a function from the derived class. This can be achieved by using the scope resolution operator `::` to specify the base class name, followed by the function name.

Example:
```cpp
class Shape {
public:
    virtual void draw() {
        std::cout << "Drawing a shape" << std::endl;
    }
};

class Circle : public Shape {
public:
    void draw() override {
        Shape::draw(); // Call the base class implementation
        std::cout << "Drawing a circle" << std::endl;
    }
};

int main() {
    Circle c;
    c.draw(); // Output: "Drawing a shape" followed by "Drawing a circle"
    return 0;
}
```
In this example, the `Circle` class overrides the `draw()` function and calls the `draw()` function in the `Shape` base class using the scope resolution operator `::`. This calls the base class implementation of the `draw()` function before executing the code in the derived class `Circle`.

### Hiding Inherited Members
When a derived class has a member with the same name as a member in the base class, the member in the derived class hides the member in the base class. This means that the member in the base class is not accessible by name in the derived class.

For example, let's modify the `Cat` class to include a new public member function play(int minutes):
```cpp
class Cat : public Animal {
public:
    void play() {
        std::cout << "Cat is playing" << std::endl;
    }
    void play(int minutes) {
        std::cout << "Cat is playing for " << minutes << " minutes" << std::endl;
    }
};
```
Now, let's create a derived class `HouseCat` and add a new public member function `play()`. This will hide the `play()` member function from the `Cat` class:
```cpp
class HouseCat : public Cat {
public:
    void play() {
        std::cout << "HouseCat is playing" << std::endl;
    }
};
```
Now, if we create an object of `HouseCat` and call the `play()` member function, the `play()` member function in the `HouseCat` class will be called instead of the `play()` member function in the `Cat` class:
```cpp
HouseCat fluffy;
fluffy.play(); // Output: "HouseCat is playing"
```
If we want to access the `play()` member function in the `Cat` class from the `HouseCat` class, we can use the scope resolution operator `::` to specify the class name:
```cpp
HouseCat fluffy;
fluffy.Cat::play(); // Output: "Cat is playing"
```

## Inheritance and Composition
In C++, inheritance and composition are two ways of building class relationships. Inheritance is an "is-a" relationship, while composition is a "has-a" relationship. In inheritance, a subclass (or derived class) is a type of its superclass (or base class), and inherits its characteristics, while in composition, a class has an instance of another class as a member variable.

### Differences Between Inheritance and Composition
Inheritance and composition are both ways of building class relationships, but they differ in terms of the nature of the relationship. Inheritance is a specialization relationship, where a subclass is a more specific version of its superclass, while composition is a containment relationship, where a class contains an instance of another class.

### When to use Inheritance vs. Composition
In general, inheritance is useful when there is a clear hierarchy of classes and subclasses, and when a subclass can be viewed as a specialized version of its superclass. On the other hand, composition is useful when a class needs to contain an instance of another class as a member variable, and when the relationship between the two classes is not hierarchical.

Example:
Consider a program that models a car dealership. We can have a `Car` class, which is the base class for different types of cars, such as `Sedan`, `SUV`, and `SportsCar`. Each of these subclasses can inherit the characteristics of the `Car` class, such as the number of doors, the fuel efficiency, and the engine type.

However, the dealership might also sell car accessories, such as GPS devices, sound systems, and air fresheners. In this case, it would be more appropriate to use composition, since the relationship between the Car class and the accessory classes is not hierarchical. We can have a `Car` class that contains a `GPSDevice` object, a `SoundSystem` object, and an `AirFreshener` object as member variables.

## Object Slicing and Object Copying
Object slicing occurs when an object of a derived class is copied to an object of its base class, resulting in the loss of derived class information. This happens because the base class object does not have the same members as the derived class object.

For example:
```cpp
class Animal {
public:
    void sleep() { std::cout << "Animal sleeping" << std::endl; }
};

class Cat : public Animal {
public:
    void meow() { std::cout << "Meow!" << std::endl; }
};

int main() {
    Cat c;
    Animal a = c; // Object slicing occurs here
    a.sleep();
    // a.meow(); // This won't compile, since a is an Animal object
    return 0;
}
```
In this example, an object of the `Cat` class is created and assigned to an object of the `Animal` class. Since `Animal` is the base class of `Cat`, the derived class information is lost, and the resulting `Animal` object only contains the members of the base class. As a result, the `meow()` function cannot be called on the `Animal` object.

To prevent object slicing, pointers or references should be used instead of actual objects. This allows the derived class information to be preserved. For example:
```cpp
int main() {
    Cat c;
    Animal* a = &c; // Use a pointer instead of an object
    a->sleep();
    static_cast<Cat*>(a)->meow(); // Use static_cast to cast back to the derived class
    return 0;
}
```
In this example, a pointer to the `Cat` object is created, and the `sleep()` function of the `Animal` class is called on it. The `meow()` function is also called on the `Cat` object using the `static_cast` operator to cast the `Animal` pointer back to a `Cat` pointer. This allows the derived class information to be preserved, preventing object slicing.