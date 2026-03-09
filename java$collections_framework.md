
# Java Collections Framework
![Collections Framework in Java](/images/collections.jpg)
## What are Collections?

Collections are containers that hold groups of objects. They provide a way to store, retrieve, and manipulate multiple items efficiently.

## Why Use Collections?

1. **Store Multiple Objects** - Hold many items in a single data structure
2. **Dynamic Size** - Automatically grow or shrink as needed
3. **Built-in Methods** - Ready-to-use operations for searching, sorting, and filtering
4. **Code Reusability** - Use proven, optimized implementations
5. **Type Safety** - Generics ensure type checking at compile time

## Common Collection Types

- **List** - Ordered, allows duplicates (ArrayList, LinkedList)
- **Set** - Unique elements only (HashSet, TreeSet)
- **Map** - Key-value pairs (HashMap, TreeMap)
- **Queue** - FIFO processing (PriorityQueue, Deque)

## Simple Example

```java
import java.util.ArrayList;
import java.util.List;
public class CollectionsExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        for (String name : names) {
            System.out.println(name);
        }
    }
}
````
