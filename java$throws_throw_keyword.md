## throw and throws in Java
### In Java, `throw` and `throws` are keywords used for exception handling, but they serve different purposes.  
### `throw` Keyword:
- The `throw` keyword is used to explicitly throw an exception from a method or a block of code. It is followed by an instance of the `Throwable` class (or its subclasses).
java throw example:
```java 
public class ThrowExample {
    static void validate(int age) {
        if (age < 18) {
            throw new ArithmeticException("Age must be at least 18 to vote.");
        } else {
            System.out.println("You are eligible to vote.");
        }
    }

    public static void main(String[] args) {
        validate(15); // This will throw an exception
    }
}
```
output:
```
Exception in thread "main" java.lang.ArithmeticException: Age must be at least 18 to vote.
    at ThrowExample.validate(ThrowExample.java:4)
    at ThrowExample.main(ThrowExample.java:10)
```
### `throws` Keyword:
- The `throws` keyword is used in a method signature to declare that a method can throw one or more exceptions. It informs the caller of the method about the potential exceptions that may be thrown, allowing them to handle those exceptions appropriately.

java throws example:
```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;
public class ThrowsExample {
    static void readFile(String fileName) throws FileNotFoundException {
        File file = new File(fileName);
        Scanner scanner = new Scanner(file);
        while (scanner.hasNextLine()) {
            System.out.println(scanner.nextLine());
        }
        scanner.close();
    }

    public static void main(String[] args) {
        try {
            readFile("nonexistentfile.txt"); // This may throw FileNotFoundException
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
```
output:
```
File not found: nonexistentfile.txt (No such file or directory)
```
### Summary:
- Use `throw` to actually throw an exception.
- Use `throws` to declare that a method may throw exceptions, allowing the caller to handle them.
