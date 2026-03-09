# ArrayList in Java

## Overview
ArrayList is a resizable array implementation in Java's Collections Framework. It's part of the `java.util` package and dynamically grows as elements are added.

## Key Features
- **Dynamic sizing** - automatically expands when needed
- **Index-based access** - O(1) retrieval by index
- **Ordered collection** - maintains insertion order
- **Not synchronized** - thread-unsafe by default

## Common Operations

### Declaration & Initialization
```java
ArrayList<String> list = new ArrayList<>();
ArrayList<Integer> numbers = new ArrayList<>(10); // initial capacity
```

### Add Elements
```java
list.add("Java");           // adds at end
list.add(0, "Python");      // adds at index 0
```

### Access Elements
```java
String element = list.get(0);
```

### Remove Elements
```java
list.remove(0);             // by index
list.remove("Java");        // by value
```

### Iteration
```java
for(String item : list) { }
for(int i = 0; i < list.size(); i++) { }
list.forEach(item -> System.out.println(item));
```

## Performance
- **Add/Remove at end**: O(1) amortized
- **Add/Remove at middle**: O(n)
- **Access**: O(1)

## When to Use
Use ArrayList when you need frequent random access and dynamic sizing with few middle insertions.
## List Interface Methods

### Index-Based Operations
```java
list.add(0, "element");           // insert at index
list.addAll(0, collection);       // insert collection at index
String element = list.get(0);     // retrieve by index
list.remove(0);                   // remove by index
list.set(0, "newElement");        // replace at index
```

### Search & Iteration
```java
int index = list.indexOf("Java");        // first occurrence
int lastIndex = list.lastIndexOf("Java"); // last occurrence
ListIterator<String> iterator = list.listIterator(); // bidirectional traversal
```

## Related Classes
- **Vector** - synchronized version of ArrayList (legacy)
- **LinkedList** - optimized for frequent insertions/deletions

## ArrayList vs Vector

| Feature | ArrayList | Vector |
|---|---|---|
| Synchronization | Non-synchronized methods | All methods synchronized |
| Thread Safety | Not thread-safe | Thread-safe |
| Performance | High (no synchronization overhead) | Low (synchronization overhead) |
| Introduction | Java 1.2 (non-legacy) | Java 1.0 (legacy) |
| Concurrent Access | Multiple threads can operate simultaneously | Only one thread at a time |

## Making ArrayList Thread-Safe

Use `Collections.synchronizedList()` to create a thread-safe ArrayList:

```java
ArrayList<String> list = new ArrayList<>();
List<String> synchronizedList = Collections.synchronizedList(list);
```

This wrapper synchronizes all operations, providing thread-safety similar to Vector with better flexibility.

## Synchronizing Collections

### ArrayList
Use `Collections.synchronizedList()` to create a thread-safe ArrayList:

```java
ArrayList<String> list = new ArrayList<>();
List<String> synchronizedList = Collections.synchronizedList(list);
```

### Set and Map
Similarly, synchronize other collection types:

```java
Set<String> synchronizedSet = Collections.synchronizedSet(new HashSet<>());
Map<String, Integer> synchronizedMap = Collections.synchronizedMap(new HashMap<>());
```

### Safe Iteration
To avoid `ConcurrentModificationException`, synchronize on the collection during iteration:

```java
List<String> list = Collections.synchronizedList(new ArrayList<>());

synchronized(list) {
    for(String item : list) {
        System.out.println(item);
    }
}
```