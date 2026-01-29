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