## 1. What is a String?
- In Java, a String is an object that represents a sequence of characters.

- It is not a primitive data type.

- Internally, it acts similarly to a character array (char[]) but provides a robust API for manipulation.

## 2. Creating Strings
- There are two primary ways to create a String object:

- String Literal: e.g., String s = "oretes";

- Stored in the String Constant Pool (SCP) within the Heap.

- Memory efficient: If the string already exists in the pool, the JVM returns the existing reference instead of creating a new object.

- Using the new Keyword: e.g., String s = new String("oretes");

- Forces the creation of a new object in the Heap memory (outside the pool).

- A literal is also placed in the pool if it isn't already there.

## 3. Immutability
- Strings are immutable, meaning once a String object is created, its value cannot be changed.

- Operations like concat() do not modify the original string; instead, they create a brand-new String object.

- This ensures security, thread safety, and allows for the String Constant Pool to function.

## 4. Key Classes and Interfaces
- Java provides the CharSequence interface, which is implemented by:

- String: Immutable; used when data shouldn't change.

- StringBuffer: Mutable and thread-safe (synchronized). Slower due to overhead; used in multi-threaded environments.

- StringBuilder: Mutable but not thread-safe. Faster than StringBuffer; preferred for single-threaded operations.

- StringTokenizer: Used to break a string into smaller tokens based on delimiters.

## 5. Memory Management
-  String Constant Pool (SCP): A special memory area in the Heap used to store literals.

-  Interning: You can manually move a string created with new into the pool using the .intern() method to save memory.

-  Historical Note: The String pool moved from PermGen (permanent generation memory) to the main Heap in newer Java versions to prevent "Out of Memory" errors.

## 6. Common Operations
- The tutorial highlights that Java's String API allows for:

- Concatenation (joining strings).

- Comparison (checking equality).

- Manipulation (substrings, changing case, etc.).

- Conversion (e.g., creating a String from a byte[] or char[]).

### Why Java Strings are Immutable?

#### In Java, strings are immutable, meaning their values cannot be changed once created. If you try to modify a string (e.g., using concat() or replace()), a new string object is created instead of altering the original one.

#### Strings are stored in a String Pool, allowing reuse of objects and reducing memory overhead.
#### Multiple threads can safely share the same string object without synchronization.
#### Immutable strings have a consistent hash code, making them reliable for use in collections like HashMap.
````java
public class oretes {
    public static void main(String[] args) {

        // Both s1 and s2 refer to the same
        // string literal in the String Pool
        String s1 = "Hello";
        String s2 = "Hello";

        // true, both point to the same object in String Pool
        System.out.println("s1 == s2: " + (s1 == s2)); 

        // Concatenation creates a new String
        // object in heap, s1 now points to it
        s1 = s1.concat(" World");

        System.out.println("s1: " + s1);      
        System.out.println("s2: " + s2);     
        System.out.println("s1 == s2: " + (s1 == s2)); 
        
        // Creating a string using new keyword stores it in the heap
        String s3 = new String("Hello");

        // false, because s2 is from String Pool and s3 is from heap
        System.out.println("s2 == s3: " + (s2 == s3)); 

        // true, because equals() compares content
        System.out.println("s2.equals(s3): " + s2.equals(s3));
    }
}
````
### Output:
```
s1 == s2: true
s1: Hello World
s2: Hello
s1 == s2: false
s2 == s3: false
s2.equals(s3): true
``` 
### Explanation:
- Initially, both `s1` and `s2` point to the same string literal "Hello" in the String Pool, so `s1 == s2` is true.
- After concatenation, `s1` points to a new string "Hello World" in the heap, while `s2` still points to "Hello", making `s1 == s2` false.
- `s3` is created using the `new` keyword, so it resides in the heap, making `s2 == s3` false. However, `s2.equals(s3)` is true because their contents are the same.

### Summary:
- Strings in Java are immutable and stored in a String Pool for memory efficiency.  
- Using the `new` keyword creates a new string object in the heap, separate from the String Pool.   
### Conclusion:
Understanding Java Strings' immutability and memory management is crucial for efficient programming and avoiding common pitfalls    
related to string manipulation and memory usage.    

Java String concat() Method with Examples
Last Updated : 20 Sep, 2025
The string concat() method concatenates (appends) a string to the end of another string. It returns the combined string. It is used for string concatenation in Java. It returns NullPointerException if any one of the strings is Null.
`````java
public class Main {
    public static void main(String[] args) {

        String firstName = "oretes";
        String lastName = "pvt_ltd";

        String fullName = firstName + " " + lastName;

        System.out.println(fullName);
    }
}
`````
### Output:
```
oretes pvt_ltd
```

## 1. length()

Returns the number of characters in the string.

## 2. charAt(int index)

Returns the character at the given index.

## 3. substring(int beginIndex)

Returns part of the string from the given index to the end.

## 4. substring(int beginIndex, int endIndex)

Returns part of the string from beginIndex to endIndex - 1.

## 5. concat(String str)

Joins the given string to the end of the current string.

## 6. indexOf(String str)

Returns the index of the first occurrence of the given string.
Returns -1 if not found.

## 7. indexOf(String str, int fromIndex)

Searches for the string starting from a specific index.

## 8. lastIndexOf(String str)

Returns the index of the last occurrence of the given string.

## 9. equals(Object obj)

Compares two strings for exact equality (case-sensitive).

## 10. equalsIgnoreCase(String str)

Compares two strings ignoring case.

## 11. compareTo(String str)

Compares two strings lexicographically (dictionary order).

## 12. compareToIgnoreCase(String str)

Same as compareTo, but ignores case differences.

## 13. toLowerCase()

Converts all characters to lowercase.

## 14. toUpperCase()

Converts all characters to uppercase.

## 15. trim()

Removes leading and trailing spaces only (not spaces between words).

## 16. replace(char oldChar, char newChar)

Replaces all occurrences of a character with another character.

## 17. contains(CharSequence seq)

Returns true if the string contains the given sequence.

## 18. toCharArray()

Converts the string into a character array.

## 19. startsWith(String prefix)

Returns true if the string starts with the given prefix.

```java 
public class StringMethodsDemo {

    public static void main(String[] args) {

        String s = "  Hello, World!  ";
        String s2 = "Hello, World!";
        String s3 = "hello, world!";
        String compareStr = "Hello, Java!";

        // 1. length()
        System.out.println("1. length(): " + s2.length());

        // 2. charAt(int index)
        System.out.println("2. charAt(7): " + s2.charAt(7));

        // 3. substring(int beginIndex)
        System.out.println("3. substring(7): " + s2.substring(7));

        // 4. substring(int beginIndex, int endIndex)
        System.out.println("4. substring(7, 12): " + s2.substring(7, 12));

        // 5. concat(String str)
        System.out.println("5. concat(): " + s2.concat("!!!"));

        // 6. indexOf(String str)
        System.out.println("6. indexOf(\"World\"): " + s2.indexOf("World"));

        // 7. indexOf(String str, int fromIndex)
        System.out.println("7. indexOf(\"l\", 4): " + s2.indexOf("l", 4));

        // 8. lastIndexOf(String str)
        System.out.println("8. lastIndexOf(\"l\"): " + s2.lastIndexOf("l"));

        // 9. equals(Object obj)
        System.out.println("9. equals(): " + s2.equals("Hello, World!"));

        // 10. equalsIgnoreCase(String str)
        System.out.println("10. equalsIgnoreCase(): " + s2.equalsIgnoreCase(s3));

        // 11. compareTo(String str)
        System.out.println("11. compareTo(): " + s2.compareTo(compareStr));

        // 12. compareToIgnoreCase(String str)
        System.out.println("12. compareToIgnoreCase(): " + s2.compareToIgnoreCase(compareStr));

        // 13. toLowerCase()
        System.out.println("13. toLowerCase(): " + s2.toLowerCase());

        // 14. toUpperCase()
        System.out.println("14. toUpperCase(): " + s2.toUpperCase());

        // 15. trim()
        System.out.println("15. trim(): '" + s.trim() + "'");

        // 16. replace(char oldChar, char newChar)
        System.out.println("16. replace(): " + s2.replace('l', 'x'));

        // 17. contains(CharSequence seq)
        System.out.println("17. contains(\"World\"): " + s2.contains("World"));

        // 18. toCharArray()
        System.out.print("18. toCharArray(): ");
        char[] chars = s2.toCharArray();
        for (char c : chars) {
            System.out.print(c + " ");
        }
        System.out.println();

        // 19. startsWith(String prefix)
        System.out.println("19. startsWith(\"Hello\"): " + s2.startsWith("Hello"));
    }
}

```
### Output:
```
1. length(): 13
2. charAt(7): W
3. substring(7): World!
4. substring(7, 12): World  
5. concat(): Hello, World!!!
6. indexOf("World"): 7
7. indexOf("l", 4): 9
8. lastIndexOf("l"): 10
9. equals(): true
10. equalsIgnoreCase(): true
11. compareTo(): 4
12. compareToIgnoreCase(): 4
13. toLowerCase(): hello, world!
14. toUpperCase(): HELLO, WORLD!
15. trim(): 'Hello, World!'
16. replace(): Hexxo, Worxd!
17. contains("World"): true
18. toCharArray(): H e l l o ,   W o r l d !
19. startsWith("Hello"): true
```

### Explanation:
- The code demonstrates the usage of various String methods in Java. Each method is called on example strings, and the results are printed to the console for clarity.
This guide provides a focused summary of the String Class in Java, breaking down its core characteristics, memory behavior, and how objects are instantiated.

### 1. Core Definition
In Java, a String is an object representing a sequence of characters. Unlike some other languages where strings are simple character arrays, Java treats them as objects of the java.lang.String class.

### Key Features
- Immutable: Once created, the content of a String object cannot be changed. Any "modification" (like toUpperCase()) actually returns a brand-new object.

- Final Class: The String class is marked as final, meaning you cannot inherit from it to create a custom String subclass.

- Thread-Safe: Because they are immutable, strings can be shared across multiple threads without the risk of data corruption or the need for synchronization.

### 2. Implemented Interfaces
- The String class is robust because it implements several key interfaces:

- CharSequence: Provides a uniform, read-only access to a sequence of characters.

- Comparable<String>: Allows strings to be compared "lexicographically" (alphabetical order) via the compareTo() method.

- Serializable: Enables strings to be converted into a byte stream for storage or network transmission.
