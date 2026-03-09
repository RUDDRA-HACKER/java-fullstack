
# Stack Methods and Stack in Collections

## What is a Stack?

A stack is a linear data structure that follows the **LIFO (Last In, First Out)** principle. The last element added is the first one to be removed.

## Stack in Java Collections

Java provides the `Stack` class in `java.util` package, which extends `Vector`.

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
```

## Common Stack Methods

| Method | Description |
|--------|-------------|
| `push(E)` | Adds an element to the top of the stack |
| `pop()` | Removes and returns the top element |
| `peek()` | Returns the top element without removing it |
| `empty()` | Checks if the stack is empty |
| `search(Object)` | Returns the position of an element |

## Example Usage

```java
Stack<String> stack = new Stack<>();

// Push elements
stack.push("A");
stack.push("B");
stack.push("C");

// Peek
System.out.println(stack.peek()); // C

// Pop
String top = stack.pop(); // C

// Check if empty
boolean isEmpty = stack.empty(); // false
```

## Use Cases

- Undo/Redo functionality
- Browser history
- Expression evaluation
- Recursive algorithms
