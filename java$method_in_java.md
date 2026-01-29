## 1. Methods in Java

#### A method is a block of code that performs a specific task. Methods help make code more organized, reusable, and easier to maintain. Every method belongs to a class in Java.

#### Key points:

- A method has a name, return type, parameters (optional), and body.

- Methods are used to avoid repeating code.

- To call a method, you either use an object (for instance methods) or the class name (for static methods).

- Java uses a call stack to manage method execution in a Last-In-First-Out (LIFO) order.

Example:
```java
public void show() {
    System.out.println("Hello!");
}
```
### 2. Static Methods vs Instance Methods

- Java has two kinds of methods based on how they are called:

- Instance Methods

- Belong to an object.

- Called on an instance of a class.

- Can access instance variables.

- Static Methods

- Belong to the class itself.

- Called using the class name.

- Cannot directly access instance variables.

Example:
``` java 
class Demo {
    static void staticMethod() { }
    void instanceMethod() { }
}
````
Demo.staticMethod();   // static
new Demo().instanceMethod();  // instance

### 3. Access Modifiers in Java

Access modifiers control visibility and access of classes, methods, and variables.

There are four main modifiers:

Modifier	Access Level
public	Anywhere (global)
private	Only within the same class
protected	Same package + subclasses
default	Same package (no keyword used)

Example:

public int x;        // visible everywhere
private int y;       // visible only in the class
protected int z;     // visible in package + subclasses
int a;               // default: package only

4. Command-Line Arguments in Java

Java allows you to pass values to a program when it starts using command-line arguments.

Syntax:

public static void main(String[] args)


Example:
If you run:

java Program Hello World


Then inside Java:

args[0] = "Hello"
args[1] = "World"


Use this to take input at startup without using Scanner or GUI.

5. Variable Arguments (Varargs) in Java

Varargs allow a method to accept any number of arguments of the same type.

Syntax:

void sum(int... numbers)


Inside the method, numbers behaves like an array.

Example:

void show(int... nums) {
    for (int n : nums) {
        System.out.println(n);
    }
}


You can call it with:

show(1, 2);
show(5, 10, 15, 20);

Overall Summary

Methods organize reusable code.

Static vs Instance Methods determines how you call the method.

Access Modifiers control access visibility.

Command-Line Arguments allow input at program start.

Varargs let a method handle a flexible number of parameters.