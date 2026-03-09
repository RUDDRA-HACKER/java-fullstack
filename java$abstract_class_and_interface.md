# Java Abstract Methods and Interfaces

## Abstract Methods

An abstract method is a method that is declared without an implementation. It must be implemented by subclasses.

### Key Characteristics
- Declared using the `abstract` keyword
- No method body (ends with semicolon)
- Can only exist in abstract classes or interfaces
- Subclasses must provide implementation

### Syntax

```java
abstract returnType methodName();
```

## Abstract Class with Abstract Method

```java
abstract class Animal {
    // Abstract method
    abstract void makeSound();
    
    // Concrete method
    void sleep() {
        System.out.println("Zzz...");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Bark!");
    }
}
```

## Interface with Abstract Methods

```java
interface Vehicle {
    void start();
    void stop();
}

class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car starting...");
    }
    
    @Override
    public void stop() {
        System.out.println("Car stopping...");
    }
}
```

## Usage Example

```java
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.makeSound();  // Output: Bark!
        dog.sleep();      // Output: Zzz...
        
        Vehicle car = new Car();
        car.start();      // Output: Car starting...
    }
}
```

## Key Points
- Cannot instantiate abstract classes directly
- Forces subclasses to implement specific methods
- Helps achieve abstraction and loose coupling

![abstract class and interface in java](/images/abstrctions.jpg)