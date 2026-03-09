## java final , finally and finalize keywords 
### In Java, final, finally, and finalize are three distinct concepts with different purposes:
1. final:
- The final keyword is used to declare constants, prevent method overriding, and prevent inheritance of classes.
- When a variable is declared as final, its value cannot be changed once assigned. 
Example:
```java
final int MAX_VALUE = 100;
```
- When a method is declared as final, it cannot be overridden by subclasses.

Example:
```java
public final void display() {
    System.out.println("This method cannot be overridden.");
}
```
output:
```
This method cannot be overridden.
```
- When a class is declared as final, it cannot be subclassed.

fianlly:
- The finally block is used in exception handling to execute a block of code regardless of whether an exception is thrown or not. It is typically used for cleanup activities like closing resources.
Example:
```java
try {
    // code that may throw an exception
} catch (Exception e) {
    // handle exception
} finally {
    // code that will always execute
}
```
finalize:
- The finalize() method is a protected method of the Object class that is called by the garbage collector before an object is removed from memory. It is used to perform cleanup operations, such as releasing resources held by the object.
Example:
```java
@Override
protected void finalize() throws Throwable {
    try {
        System.out.println("Object is being garbage collected.");
    } finally {
        super.finalize();
    }
}
```
output:
```
Object is being garbage collected.
```