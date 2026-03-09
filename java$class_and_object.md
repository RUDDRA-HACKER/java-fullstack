
# Java Classes and Objects

## What is a Class?
A class is a blueprint or template for creating objects. It defines properties (attributes) and behaviors (methods).

```java
public class Car {
    // Attributes
    private String color;
    private String model;
    
    // Method
    public void drive() {
        System.out.println("Car is driving");
    }
}
```

## What is an Object?
An object is an instance of a class. It's a concrete realization of the class blueprint.

```java
// Creating an object
Car myCar = new Car();
myCar.drive();
```

## Key Differences

| Class | Object |
|-------|--------|
| Logical entity | Physical entity |
| Declared once | Multiple objects can be created |
| No memory allocated | Memory allocated when created |
| Template | Instance of a template |

## Constructor
Constructors initialize objects when they are created.

```java
public class Car {
    private String color;
    
    public Car(String color) {
        this.color = color;
    }
}
```

## Encapsulation
Encapsulation is the bundling of data and methods that operate on that data within a single unit (class), hiding internal details from the outside world.

```java
public class Car {
    private String color; // Private attribute
    
    public String getColor() {
        return color;
    }
    
    public void setColor(String color) {
        this.color = color;
    }
}
```

## Inheritance
Inheritance allows a class to inherit properties and methods from another class, promoting code reusability.

```java
public class Vehicle {
    public void start() {
        System.out.println("Vehicle started");
    }
}

public class Car extends Vehicle {
    // Inherits start() method
}
```

## Polymorphism
Polymorphism allows methods to have multiple forms, enabling the same method name to behave differently based on context.

```java
public class Animal {
    public void sound() {
        System.out.println("Some sound");
    }
}

public class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Bark");
    }
}
```

## Abstraction
Abstraction hides complex implementation details and shows only essential features to the user.

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing circle");
    }
}
```
![Classes and Objects in Java](/images/class.jpg)