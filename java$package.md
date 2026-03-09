# Java Packages

## What is a Package?

A package in Java is a namespace that organizes a set of related classes and interfaces. Packages help avoid naming conflicts and provide a way to organize code logically.

## Key Benefits

- **Organization**: Group related classes together
- **Namespace Management**: Avoid class name conflicts
- **Access Control**: Control visibility with package-private access
- **Reusability**: Better code organization for reuse

## Creating a Package

```java
package com.example.utils;

public class StringHelper {
    public static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
}
```

## Using a Package (Import)

```java
import com.example.utils.StringHelper;

public class Main {
    public static void main(String[] args) {
        String result = StringHelper.reverse("Hello");
        System.out.println(result); // Output: olleH
    }
}
```

## Package Naming Convention

- All lowercase
- Reverse domain name format: `com.company.project.module`
- Example: `java.util`, `javax.swing`

## Built-in Packages

| Package | Purpose |
|---------|---------|
| `java.lang` | Core language classes (default import) |
| `java.util` | Collections, utilities |
| `java.io` | Input/Output operations |
| `java.time` | Date and time |

![Packages in Java](/images/unnamed1.jpg)