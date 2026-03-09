# Constructors of Vector Class

1. **`Vector v = new Vector();`**
    - Creates an empty vector with default initial capacity of 10
    - When full, capacity doubles: `newCapacity = 2 * currentCapacity`

2. **`Vector v = new Vector(int initialCapacity);`**
    - Creates an empty Vector with specified initial capacity

3. **`Vector v = new Vector(int initialCapacity, int incrementalCapacity);`**
    - Creates an empty Vector with custom initial capacity
    - Growth behavior: `newCapacity = currentCapacity + incrementalCapacity`

4. **`Vector v = new Vector(Collection c);`**
    - Creates a Vector containing all elements from the given Collection

## Example: incrementalCapacity vs Default Growth

```java
// Default doubling behavior
Vector<Integer> v1 = new Vector<>(); // capacity=10, grows by 2x

// Custom incremental growth
Vector<Integer> v2 = new Vector<>(10, 5); // capacity=10, grows by +5
```

When full:
- `v1`: 10 → 20 → 40 → 80...
- `v2`: 10 → 15 → 20 → 25...

