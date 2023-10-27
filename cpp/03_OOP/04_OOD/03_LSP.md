
### Liskov Substitution Principle (LSP)
The Liskov Substitution Principle (LSP) is a fundamental principle of object-oriented design that states that objects of a superclass should be replaceable with objects of its subclasses without causing errors or unexpected behavior in the program.

#### Understanding the Concept of Substitutability
Substitutability is the ability of a derived class to replace its base class without affecting the correctness of the program. In other words, if a program is designed to work with objects of a base class, it should also work correctly with objects of any of its derived classes.

To adhere to LSP, derived classes should satisfy the following conditions:
* They should preserve the behavior of the base class. This means that any method or property of the base class should still work correctly with objects of the derived class.
* They should not add any new preconditions to the methods of the base class. A precondition is a condition that must be true before a method can be executed. Derived classes should not add any new preconditions that were not present in the base class.
* They should not weaken any of the postconditions of the methods of the base class. A postcondition is a condition that must be true after a method has executed. Derived classes should not make any postconditions weaker than they were in the base class.
* They should not introduce any new exceptions that are not part of the base class's exception hierarchy. Derived classes should not introduce new exceptions that were not already part of the exception hierarchy of the base class.

#### Examples of applying LSP in C++ inheritance hierarchies:
Consider a base class `Animal` with a virtual function `makeSound()`. We can create derived classes `Dog` and `Cat` that override the `makeSound()` function with their own implementations. If we have a function that accepts an `Animal` object and calls its `makeSound()` function, we should be able to pass in a `Dog` or `Cat` object without affecting the correctness of the program.

Another example is a `Rectangle` and a `Square` class. A square might be considered a special type of a rectangle where its width and height are equal. Creating classes using assumption leads to
```cpp
#include <iostream>

class Rectangle {
public:
    virtual void setWidth(double w) { width_ = w; }
    virtual void setHeight(double h) { height_ = h; }
    virtual double getWidth() const { return width_; }
    virtual double getHeight() const { return height_; }
    double area() const { return width_ * height_; }

protected:
    double width_;
    double height_;
};

class Square : public Rectangle {
public:
    void setWidth(double w) override { width_ = height_ = w; }
    void setHeight(double h) override { height_ = width_ = h; }
};

void printArea(Rectangle& r) {
    r.setWidth(5);
    r.setHeight(10);
    std::cout << "Area: " << r.area() << std::endl;
}

int main() {
    Rectangle rect;
    Square square;
    printArea(rect);  // output: Area: 50
    printArea(square); // output: Area: 50, but expected Area: 25

    return 0;
}
```
In this example, the `Square` class inherits from the `Rectangle` class, which has `setWidth` and `setHeight` methods that allow the width and height of the rectangle to be set independently. However, in the `Square` class, both `setWidth` and `setHeight` methods set both the width and height to the same value, since a square has equal sides. This violates the Liskov Substitution Principle (LSP), as substituting a `Square` for a Rectangle in the `printArea` function produces unexpected results.

To fix this, we can create an intermediate Shape class that is responsible for calculating the area, and make Rectangle and Square inherit from it:
```cpp
#include <iostream>

class Shape {
public:
    virtual double area() const = 0;
};

class Rectangle : public Shape {
public:
    Rectangle(double w, double h) : width_(w), height_(h) {}
    void setWidth(double w) { width_ = w; }
    void setHeight(double h) { height_ = h; }
    double getWidth() const { return width_; }
    double getHeight() const { return height_; }
    double area() const override { return width_ * height_; }

private:
    double width_;
    double height_;
};

class Square : public Shape {
public:
    Square(double side) : side_(side) {}
    void setSide(double side) { side_ = side; }
    double getSide() const { return side_; }
    double area() const override { return side_ * side_; }

private:
    double side_;
};

void printArea(Shape& s) {
    std::cout << "Area: " << s.area() << std::endl;
}

int main() {
    Rectangle rect(5, 10);
    Square square(5);

    printArea(rect);   // output: Area: 50
    printArea(square); // output: Area: 25

    return 0;
}
```
Now, the `Rectangle` and `Square` classes both inherit from the `Shape` class and implement the `area` method appropriately. Substituting a `Square` for a `Rectangle` in the `printArea` function produces the expected result.

Violating the Liskov Substitution Principle can lead to errors and unexpected behavior in the program. If a derived class does not properly adhere to the behavior of the base class, it can cause functions that work with the base class to fail when working with objects of the derived class. This can lead to errors that are difficult to debug and fix. Therefore, it is important to design and implement derived classes in a way that adheres to the Liskov Substitution Principle.