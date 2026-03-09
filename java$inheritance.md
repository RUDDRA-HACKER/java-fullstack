
# Java Inheritance

Inheritance is a mechanism where a new class derives properties and behaviors from an existing class.

## Key Concepts

- **Superclass (Parent Class)**: The class being inherited from
- **Subclass (Child Class)**: The class that inherits from the superclass
- **Keyword**: `extends`

## Syntax

```java
class Child extends Parent {
    // child class members
}
```

## Example

```java
// Parent class
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

// Child class
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();   // inherited from Animal
        dog.bark();  // from Dog
    }
}
```

## Types of Inheritance

1. **Single**: One class extends one class
2. **Multilevel**: A → B → C
3. **Hierarchical**: Multiple classes extend one class
4. **Multiple**: Not directly supported (use interfaces instead)

## Benefits

- Code reusability
- Method overriding
- Polymorphism support

![Inheritance in Java](/images/inheritance.jpg)