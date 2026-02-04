## Interface

### An interface is a collection of method declarations that defines what a class should do, but not how it should do it.

### Before Java 8, interfaces could only have abstract methods (no bodies). Since Java 8, they can also include default and static methods (with implementation) and since Java 9, private methods are allowed.

A class can extend another class and similarly, an interface can extend another interface. However, only a class can implement an interface and the reverse (an interface implementing a class) is not allowed.

### Syntax of Interface

```java 
interface InterfaceName {
    // abstract method
    void method1();

    // default method
    default void method2() {
        // method body
    }

    // static method
    static void method3() {
        // method body
    }
}
```
### Implementing an Interface

```java
class ClassName implements InterfaceName {
    // providing implementation for abstract method
    public void method1() {
        // method body
    }
}
```
### Key Points about Interfaces
- A class can implement multiple interfaces, allowing for multiple inheritance of type. 
- All methods in an interface are implicitly public and abstract (except default and static methods).
- Interfaces can contain constants (static final variables).    
- Interfaces cannot have instance variables.
- A class that implements an interface must provide implementations for all abstract methods declared in the interface.
- Interfaces are used to achieve abstraction and define a contract for classes to follow.
### Example of Interface

```java
interface Animal {
    void sound(); // abstract method
}
class Dog implements Animal {
    public void sound() {
        System.out.println("Woof");
    }
}
class Cat implements Animal {
    public void sound() {
        System.out.println("Meow");
    }
}
public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.sound(); // Output: Woof

        Animal cat = new Cat();
        cat.sound(); // Output: Meow
    }
}
``` 
### In this example, the `Animal` interface defines an abstract method `sound()`. The `Dog` and `Cat` classes implement the `Animal` interface and provide their own implementations of the `sound()` method.
### This allows for polymorphism, as we can treat different animal types uniformly through the `Animal` interface.  
## class vs interface   
| Feature               | Class                              | Interface                          |
|-----------------------|------------------------------------|------------------------------------| 
| Inheritance           | A class can extend only one class. | An interface can extend multiple interfaces. |
| Implementation        | A class can implement multiple interfaces. | An interface cannot implement a class.
| Method Types          | Can have concrete methods (with body) and abstract methods. | Can have abstract methods, default methods, static methods, and private methods. |
| Variables             | Can have instance variables.       | Can only have static final variables (constants). |
| Access Modifiers      | Can have various access modifiers (public, private, protected). || Object Creation       | Can be instantiated to create objects. | Cannot be instantiated directly. |
| Purpose               | Used to represent real-world entities with state and behavior. | Used to define a contract for classes to implement. |

### In summary, classes are used to create objects with specific behaviors and states, while interfaces define a contract that classes must follow without dictating how those behaviors are implemented.

## functional interface
A functional interface is an interface that contains exactly one abstract method. They can have multiple default or static methods, but only one abstract method. Functional interfaces are used primarily in lambda expressions and method references in Java. 
### Syntax of Functional Interface

```java
@FunctionalInterface
interface FunctionalInterfaceName {
    void abstractMethod(); // single abstract method

    // default method
    default void defaultMethod() {
        // method body
    }

    // static method
    static void staticMethod() {
        // method body
    }
}
``` 
### Example of Functional Interface

```java
@FunctionalInterface
interface MathOperation {
    int operation(int a, int b); // single abstract method
}
class Calculator {
    public int executeOperation(int a, int b, MathOperation op) {
        return op.operation(a, b);
    }
}
public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        // Using lambda expression to define the operation
        MathOperation addition = (a, b) -> a + b;
        MathOperation subtraction = (a, b) -> a - b;

        System.out.println("Addition: " + calculator.executeOperation(5, 3, addition)); // Output: 8
        System.out.println("Subtraction: " + calculator.executeOperation(5, 3, subtraction)); // Output: 2
    }
}
```
### In this example, the `MathOperation` interface is a functional interface with a single abstract method `operation()`. The `Calculator` class uses this interface to perform different mathematical operations defined using lambda expressions.
### The `@FunctionalInterface` annotation is optional but recommended, as it helps to ensure that the interface meets the criteria of a functional interface by generating a compile-time error if it does not. 
### Functional interfaces are widely used in Java's functional programming features, such as the Stream API and the `java.util.function` package, which provides several built-in functional interfaces like `Predicate`, `Function`, `Consumer`, and `Supplier`.
## default methods in interface
Default methods were introduced in Java 8 to allow developers to add new methods to interfaces without breaking the existing implementations of those interfaces. A default method is defined in an interface using the `default` keyword and provides a default implementation that can be used by classes that implement the interface.
### Syntax of Default Method

```java 
interface InterfaceName {
    // default method
    default void defaultMethod() {
        // method body
    }
}
``` 
### Example of Default Method

```java
interface Vehicle {
    void start(); // abstract method

    default void stop() { // default method
        System.out.println("Vehicle stopped.");
    }
}
class Car implements Vehicle {
    public void start() {
        System.out.println("Car started.");
    }
}   
public class Main {
    public static void main(String[] args) {
        Vehicle myCar = new Car();
        myCar.start(); // Output: Car started.
        myCar.stop();  // Output: Vehicle stopped.
    }
}
```
### In this example, the `Vehicle` interface defines an abstract method `start()` and a default method `stop()`. The `Car` class implements the `Vehicle` interface and provides its own implementation for the `start()` method. However, it inherits the default implementation of the `stop()` method from the interface.
### This allows for backward compatibility, as existing classes that implement the `Vehicle` interface do not need to provide an implementation for the new `stop()` method unless they want to override it with their own behavior.
### If a class implements multiple interfaces that contain default methods with the same signature, the class must override the conflicting default method to resolve the ambiguity.
### Example of Resolving Default Method Conflict

```java 
interface InterfaceA {
    default void display() {
        System.out.println("Interface A display");
    }
}
interface InterfaceB {
    default void display() {
        System.out.println("Interface B display");
    }
}
class MyClass implements InterfaceA, InterfaceB {
    @Override
    public void display() {
        // Resolving conflict by providing own implementation
        System.out.println("MyClass display");
    }
}
public class Main {
    public static void main(String[] args) {
        MyClass myObject = new MyClass();
        myObject.display(); // Output: MyClass display
    }
}
```
### output   
```
MyClass display
```
### In this example, `MyClass` implements both `InterfaceA` and `InterfaceB`, which have conflicting default methods named `display()`. To resolve the conflict, `MyClass` provides its own implementation of the `display()` method.
### Default methods are a powerful feature that enhances the flexibility of interfaces in Java, allowing for easier evolution of APIs while maintaining compatibility with existing code.

## static methods in interface
Static methods in interfaces were also introduced in Java 8. They allow you to define methods that belong to the interface itself rather than to any instance of a class that implements the interface. Static methods can be called directly on the interface without needing an instance of a class.
### Syntax of Static Method

```java
interface InterfaceName {
    // static method
    static void staticMethod() {
        // method body
    }
}
``` 
### Example of Static Method

```java
interface MathUtils {
    static int add(int a, int b) { // static method
        return a + b;
    }
}
public class Main {
    public static void main(String[] args) {
        // Calling the static method directly on the interface
        int sum = MathUtils.add(5, 3);
        System.out.println("Sum: " + sum); // Output: Sum: 8
    }
}
``` 
### In this example, the `MathUtils` interface defines a static method `add()`. The `Main` class calls this static method directly on the `MathUtils` interface without needing to create an instance of any class.
### Static methods in interfaces are useful for providing utility functions related to the interface's purpose. They can help organize code and avoid the need for separate utility classes.
### Note that static methods in interfaces cannot be overridden by implementing classes. They are bound to the interface itself and can only be accessed using the interface name.
