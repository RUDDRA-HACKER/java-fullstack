## Exception Handling in Java
### What is Exception Handling?
### Exception handling in Java is a mechanism that allows developers to manage runtime errors, ensuring the normal flow of the application. It helps in gracefully handling unexpected situations without crashing the program.
### An exception is an event that disrupts the normal flow of a program's execution. It can occur due to various reasons, such as invalid input, resource unavailability, or programming errors.
### Types of Exceptions
### 1. Checked Exceptions: These are exceptions that are checked at compile-time. The programmer is required to handle these exceptions using try-catch blocks or by declaring them in the method signature using the throws keyword. Examples include IOException, SQLException, etc.
### 2. Unchecked Exceptions: These are exceptions that occur at runtime and are not checked at compile-time. They are usually caused by programming errors, such as logic mistakes or improper use of APIs. Examples include NullPointerException, ArrayIndexOutOfBoundsException, etc.
### 3. Errors: These are serious issues that are not meant to be caught by applications. They usually indicate problems with the Java Virtual Machine (JVM) itself, such as OutOfMemoryError or StackOverflowError.
### Key Components of Exception Handling                
### 1. try block: The code that might throw an exception is placed inside a try block. If an exception occurs, the control is transferred to the corresponding catch block.
### 2. catch block: This block is used to handle the exception thrown by the try block. You can have multiple catch blocks to handle different types of exceptions.
### 3. finally block: This block is optional and is used to execute code that must run regardless of whether an exception occurred or not. It is typically used for cleanup activities, such as closing resources.
### 4. throw statement: This is used to explicitly throw an exception from a method or a block of code.
### 5. throws keyword: This is used in method signatures to declare that a method can throw certain types of exceptions.
### Example of Exception Handling in Java
```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int[] numbers = {1, 2, 3};
            System.out.println(numbers[5]); // This will throw ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index is out of bounds: " + e.getMessage());
        } finally {
            System.out.println("Execution completed.");
        }
    }
}
```
## output:  
```
Array index is out of bounds: 5
Execution completed.
```
## java hirarchy of Exception classes
### In Java, all exception classes are derived from the java.lang.Throwable class. The hierarchy is as follows:
1. Throwable
   - Error
     - VirtualMachineError
       - OutOfMemoryError
       - StackOverflowError
   - Exception
     - IOException
       - FileNotFoundException
     - SQLException
     - RuntimeException
       - NullPointerException
       - ArrayIndexOutOfBoundsException
       - ArithmeticException    
### Best Practices for Exception Handling
1. Catch specific exceptions rather than using a generic Exception class.   
2. Use finally blocks to release resources like file handles or database connections.
3. Avoid using exceptions for control flow in your program.
4. Log exceptions for debugging and maintenance purposes.
5. Provide meaningful messages when throwing exceptions to help diagnose issues.

![exeption-handling](/images/Exceptions-in-Java.webp)

