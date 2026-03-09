
# Polymorphism in Java

## Definition
Polymorphism means "many forms." It allows objects to take multiple forms and enables you to write flexible, reusable code.

## Types of Polymorphism

### 1. Compile-time Polymorphism (Method Overloading)
Method overloading occurs when multiple methods have the same name but different parameters.

```java
public class Calculator {
    // Method 1
    public int add(int a, int b) {
        return a + b;
    }
    
    // Method 2 - different parameter types
    public double add(double a, double b) {
        return a + b;
    }
    
    // Method 3 - different number of parameters
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

### 2. Runtime Polymorphism (Method Overriding)
Method overriding occurs when a subclass provides its own implementation of a superclass method.

```java
// Parent class
public class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

// Child class 1
public class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks: Woof!");
    }
}

// Child class 2
public class Cat extends Animal {
    @Override
    public void sound() {
        System.out.println("Cat meows: Meow!");
    }
}

// Usage example
public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        Animal myCat = new Cat();
        
        myDog.sound();  // Output: Dog barks: Woof!
        myCat.sound();  // Output: Cat meows: Meow!
    }
}
```

## Benefits
- **Code Reusability**: Write once, use in multiple contexts
- **Flexibility**: Easy to extend and maintain
- **Loose Coupling**: Reduces dependencies between classes

![Polymorphism in Java](/images/unnamed.jpg)