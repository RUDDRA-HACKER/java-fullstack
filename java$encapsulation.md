
# Encapsulation in Java

## Overview
Encapsulation is one of the four OOP concepts in Java. It binds data (variables) and methods together and hides implementation details from the outside world using access modifiers.

## Key Points
- **Data Hiding**: Keep fields private
- **Controlled Access**: Provide public getter/setter methods
- **Maintainability**: Change internal implementation without affecting external code
- **Security**: Protect object integrity

## Access Modifiers
- `private`: Accessible only within the class
- `public`: Accessible from anywhere
- `protected`: Accessible within package and subclasses
- default (no modifier): Accessible within package

## Simple Example

```java
public class Student {
    // Private variables
    private String name;
    private int age;
    private double gpa;

    // Getter methods
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public double getGpa() {
        return gpa;
    }

    // Setter methods with validation
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        }
    }

    public void setAge(int age) {
        if (age > 0 && age < 100) {
            this.age = age;
        }
    }

    public void setGpa(double gpa) {
        if (gpa >= 0.0 && gpa <= 4.0) {
            this.gpa = gpa;
        }
    }
}
```

## Usage
```java
Student student = new Student();
student.setName("John");
student.setAge(20);
student.setGpa(3.8);

System.out.println(student.getName()); // John
```
![Encapsulation in Java](/images/encapsulations.jpg)