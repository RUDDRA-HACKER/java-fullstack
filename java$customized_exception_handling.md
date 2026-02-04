## user defined exception class
### Creating a Custom Exception
To create a custom exception in Java, you need to define a new class that extends the `Exception` class (or one of its subclasses). Here's an example of how to create and use a custom exception:

```java
// Custom exception class
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```
### Using the Custom Exception
You can use the custom exception in your code by throwing it when a specific condition is met. Here's an example of how to use the `InvalidAgeException`:

```java
public class CustomExceptionExample {
    // Method to validate age
    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be at least 18.");
        } else {
            System.out.println("Valid age: " + age);
        }
    }

    public static void main(String[] args) {
        try {
            validateAge(15); // This will throw the custom exception
        } catch (InvalidAgeException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }

        try {
            validateAge(20); // This will pass
        } catch (InvalidAgeException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```
### Output
When you run the above code, the output will be:
```
Caught exception: Age must be at least 18.
Valid age: 20.
```
### Explanation
1. We defined a custom exception class `InvalidAgeException` that extends the `Exception` class.
2. The `validateAge` method checks if the provided age is less than 18. If it is, it throws an `InvalidAgeException` with a relevant message.
3. In the `main` method, we call `validateAge` with different age values and handle the custom exception using a try-catch block.   
This demonstrates how to create and use customized exception handling in Java.
