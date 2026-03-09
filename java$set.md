# Java Set Collections — Complete Notes

> **Topic:** Java Collection Framework — Set Interface
> **Subject:** Core Java

---

## What is a Set?

A **Set** is a collection that:
- Does **NOT allow duplicate elements**
- At most **one `null` value** is allowed
- Does **NOT guarantee insertion order** (except LinkedHashSet)

Set is a **child interface** of the `Collection` interface.

```
Collection
    └── Set
            ├── HashSet
            │       └── LinkedHashSet
            ├── SortedSet
            │       └── NavigableSet
            │               └── TreeSet
```

---

## 1. HashSet

### What is HashSet?

**HashSet** is the most commonly used Set in Java.

Think of it like a **bag** — you can throw items in, but:
- No duplicates allowed
- Items have **no fixed order** (order changes randomly)
- Very **fast** for searching and adding

### Key Points

| Property | Value |
|----------|-------|
| Duplicates | ❌ Not allowed |
| Insertion Order | ❌ Not maintained |
| Null values | ✅ One null allowed |
| Sorting | ❌ No sorting |
| Thread Safe | ❌ No |
| Internal Structure | **Hashtable** |
| Introduced in | Java 1.2 |

### How to Create a HashSet

```java
// Default — initial capacity 16, load factor 0.75
HashSet<String> hs = new HashSet<>();

// Custom initial capacity
HashSet<String> hs = new HashSet<>(32);

// Custom capacity and load factor
HashSet<String> hs = new HashSet<>(32, 0.5f);

// Create from another collection
HashSet<String> hs = new HashSet<>(existingList);
```

> 💡 **Load Factor** means: when the HashSet is 75% full, it automatically increases its size. Default is `0.75`.

### HashSet Methods

| Method | What it does |
|--------|-------------|
| `add(Object o)` | Adds element, returns `false` if duplicate |
| `remove(Object o)` | Removes the element |
| `contains(Object o)` | Returns `true` if element exists |
| `size()` | Returns number of elements |
| `isEmpty()` | Returns `true` if empty |
| `clear()` | Removes all elements |
| `iterator()` | Returns an Iterator |
| `addAll(Collection c)` | Adds all elements from another collection |
| `removeAll(Collection c)` | Removes all matching elements |
| `retainAll(Collection c)` | Keeps only matching elements |
| `toArray()` | Converts to array |

### HashSet Examples

#### Example 1 — Basic Add and Duplicates

```java
import java.util.*;

public class HashSetBasic {
    public static void main(String[] args) {

        HashSet<String> hs = new HashSet<>();

        hs.add("Banana");
        hs.add("Apple");
        hs.add("Mango");
        hs.add("Apple");   // duplicate — will be ignored
        hs.add(null);      // null is allowed

        System.out.println(hs);
        System.out.println("Size: " + hs.size());
    }
}
```

**Output:**
```
[null, Mango, Banana, Apple]
Size: 4
```
> Notice: "Apple" added twice but appears once. Order is random.

---

#### Example 2 — contains() and remove()

```java
import java.util.*;

public class HashSetMethods {
    public static void main(String[] args) {

        HashSet<Integer> hs = new HashSet<>();
        hs.add(10);
        hs.add(20);
        hs.add(30);
        hs.add(40);

        System.out.println("Contains 20? " + hs.contains(20));  // true
        System.out.println("Contains 99? " + hs.contains(99));  // false

        hs.remove(20);
        System.out.println("After removing 20: " + hs);

        System.out.println("Is empty? " + hs.isEmpty());  // false
        hs.clear();
        System.out.println("After clear: " + hs);         // []
    }
}
```

**Output:**
```
Contains 20? true
Contains 99? false
After removing 20: [10, 30, 40]
Is empty? false
After clear: []
```

---

#### Example 3 — Iterating HashSet

```java
import java.util.*;

public class HashSetIterate {
    public static void main(String[] args) {

        HashSet<String> hs = new HashSet<>();
        hs.add("Red");
        hs.add("Green");
        hs.add("Blue");

        // Method 1 — for-each loop
        System.out.println("Using for-each:");
        for (String color : hs) {
            System.out.println(color);
        }

        // Method 2 — Iterator
        System.out.println("Using Iterator:");
        Iterator<String> itr = hs.iterator();
        while (itr.hasNext()) {
            System.out.println(itr.next());
        }
    }
}
```

---

#### Example 4 — Set Operations (Union, Intersection, Difference)

```java
import java.util.*;

public class HashSetOperations {
    public static void main(String[] args) {

        HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
        HashSet<Integer> set2 = new HashSet<>(Arrays.asList(4, 5, 6, 7, 8));

        // Union — all elements from both
        HashSet<Integer> union = new HashSet<>(set1);
        union.addAll(set2);
        System.out.println("Union: " + union);

        // Intersection — only common elements
        HashSet<Integer> intersection = new HashSet<>(set1);
        intersection.retainAll(set2);
        System.out.println("Intersection: " + intersection);

        // Difference — elements in set1 but not in set2
        HashSet<Integer> difference = new HashSet<>(set1);
        difference.removeAll(set2);
        System.out.println("Difference: " + difference);
    }
}
```

**Output:**
```
Union:        [1, 2, 3, 4, 5, 6, 7, 8]
Intersection: [4, 5]
Difference:   [1, 2, 3]
```

---

### Internal Working of HashSet

HashSet internally uses a **HashMap**. When you add an element:

1. Java calls `hashCode()` on the element
2. It finds the correct **bucket** using the hash
3. If the bucket is empty — element is stored
4. If the bucket has elements — Java calls `equals()` to check for duplicates
5. If duplicate found — element is **rejected**
6. If not duplicate — element is stored

```
add("Apple")  →  hashCode("Apple") = 63476538
                 bucket = 63476538 % 16 = 10
                 bucket 10 is empty → store "Apple"

add("Apple")  →  hashCode("Apple") = 63476538
                 bucket 10 → "Apple" already there
                 equals() returns true → REJECTED (duplicate)
```

> 💡 This is why HashSet is **very fast** — it uses hashing to find elements in O(1) time.

---

## 2. LinkedHashSet

### What is LinkedHashSet?

**LinkedHashSet** is a child class of HashSet.

It is exactly like HashSet but with **one extra feature** — it **maintains insertion order**.

Think of it like a **queue with no duplicates** — items are stored in the order you added them.

### Key Points

| Property | Value |
|----------|-------|
| Duplicates | ❌ Not allowed |
| Insertion Order | ✅ **Maintained** |
| Null values | ✅ One null allowed |
| Sorting | ❌ No sorting |
| Thread Safe | ❌ No |
| Internal Structure | **HashTable + LinkedList** |
| Introduced in | Java 1.4 |
| Parent class | HashSet |

### HashSet vs LinkedHashSet

| Feature | HashSet | LinkedHashSet |
|---------|---------|---------------|
| Order | ❌ Random | ✅ Insertion order |
| Speed | Slightly faster | Slightly slower |
| Memory | Less | More (stores links) |
| Use when | Order doesn't matter | Order matters |

### How to Create LinkedHashSet

```java
LinkedHashSet<String> lhs = new LinkedHashSet<>();

// Custom capacity
LinkedHashSet<String> lhs = new LinkedHashSet<>(32);

// Custom capacity and load factor
LinkedHashSet<String> lhs = new LinkedHashSet<>(32, 0.5f);
```

### LinkedHashSet Examples

#### Example 1 — Insertion Order Maintained

```java
import java.util.*;

public class LinkedHashSetBasic {
    public static void main(String[] args) {

        // HashSet — no order
        HashSet<String> hs = new HashSet<>();
        hs.add("Banana");
        hs.add("Apple");
        hs.add("Mango");
        hs.add("Cherry");
        System.out.println("HashSet:       " + hs);

        // LinkedHashSet — insertion order
        LinkedHashSet<String> lhs = new LinkedHashSet<>();
        lhs.add("Banana");
        lhs.add("Apple");
        lhs.add("Mango");
        lhs.add("Cherry");
        System.out.println("LinkedHashSet: " + lhs);
    }
}
```

**Output:**
```
HashSet:       [Mango, Cherry, Apple, Banana]   ← random order
LinkedHashSet: [Banana, Apple, Mango, Cherry]   ← insertion order preserved
```

---

#### Example 2 — Duplicate Handling

```java
import java.util.*;

public class LinkedHashSetDuplicate {
    public static void main(String[] args) {

        LinkedHashSet<String> lhs = new LinkedHashSet<>();
        lhs.add("Java");
        lhs.add("Python");
        lhs.add("Java");    // duplicate — ignored
        lhs.add("C++");
        lhs.add("Python");  // duplicate — ignored
        lhs.add(null);

        System.out.println(lhs);
        System.out.println("Size: " + lhs.size());
    }
}
```

**Output:**
```
[Java, Python, C++, null]
Size: 4
```

---

#### Example 3 — Remove Duplicates from a List (Practical Use)

```java
import java.util.*;

public class RemoveDuplicates {
    public static void main(String[] args) {

        List<Integer> listWithDuplicates = Arrays.asList(5, 3, 1, 3, 5, 7, 1, 9);
        System.out.println("Original List: " + listWithDuplicates);

        // Use LinkedHashSet to remove duplicates and keep order
        LinkedHashSet<Integer> lhs = new LinkedHashSet<>(listWithDuplicates);
        System.out.println("After removing duplicates: " + lhs);

        // Convert back to List if needed
        List<Integer> result = new ArrayList<>(lhs);
        System.out.println("Back to List: " + result);
    }
}
```

**Output:**
```
Original List:            [5, 3, 1, 3, 5, 7, 1, 9]
After removing duplicates: [5, 3, 1, 7, 9]
Back to List:              [5, 3, 1, 7, 9]
```

> 💡 This is the most common **real-world use** of LinkedHashSet — removing duplicates while keeping order.

---

### Internal Working of LinkedHashSet

LinkedHashSet internally uses a **LinkedHashMap**.

It maintains a **doubly linked list** running through all entries. This linked list defines the iteration order — which is the order in which elements were inserted.

```
Insertion: "A" → "B" → "C"

Internal structure:
[A] ⟷ [B] ⟷ [C]
 ↑                ↑
Head             Tail

Iteration gives: A, B, C  (same as insertion order)
```

---

## 3. SortedSet

### What is SortedSet?

**SortedSet** is a child interface of Set that **sorts elements automatically**.

Think of it like a **sorted bag** — whenever you add an item, it automatically goes to the right sorted position.

### Key Points

| Property | Value |
|----------|-------|
| Duplicates | ❌ Not allowed |
| Insertion Order | ❌ Not maintained |
| Sorting | ✅ **Automatic sorting** |
| Null values | ❌ Not allowed (throws NullPointerException) |
| Type | **Interface** (not a class) |
| Implemented by | `TreeSet` |

> ⚠️ SortedSet is an **interface** — you cannot create it directly. You use `TreeSet` which implements it.

### SortedSet Specific Methods

These methods are extra — only available in SortedSet (not in regular Set):

| Method | What it does |
|--------|-------------|
| `first()` | Returns the **smallest** (first) element |
| `last()` | Returns the **largest** (last) element |
| `headSet(Object o)` | Returns elements **less than** `o` |
| `tailSet(Object o)` | Returns elements **greater than or equal to** `o` |
| `subSet(Object o1, Object o2)` | Returns elements from `o1` (inclusive) to `o2` (exclusive) |
| `comparator()` | Returns the Comparator used, or `null` if natural order |

---

## 4. TreeSet (Implementation of SortedSet)

### What is TreeSet?

**TreeSet** is the implementation class of SortedSet.

It stores elements in **sorted order** (ascending by default).

### Key Points

| Property | Value |
|----------|-------|
| Duplicates | ❌ Not allowed |
| Insertion Order | ❌ Not maintained |
| Sorting | ✅ **Natural ascending order by default** |
| Null values | ❌ Not allowed |
| Thread Safe | ❌ No |
| Internal Structure | **Red-Black Tree** |
| Introduced in | Java 1.2 |

### How to Create TreeSet

```java
// Default — natural sorting (ascending)
TreeSet<Integer> ts = new TreeSet<>();

// Custom sorting using Comparator
TreeSet<Integer> ts = new TreeSet<>(Comparator.reverseOrder());

// From another collection
TreeSet<String> ts = new TreeSet<>(existingList);
```

### TreeSet Examples

#### Example 1 — Natural Sorting

```java
import java.util.*;

public class TreeSetBasic {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(50);
        ts.add(10);
        ts.add(40);
        ts.add(20);
        ts.add(30);
        ts.add(10);   // duplicate — ignored

        System.out.println("TreeSet: " + ts);
        System.out.println("First:   " + ts.first());
        System.out.println("Last:    " + ts.last());
    }
}
```

**Output:**
```
TreeSet: [10, 20, 30, 40, 50]
First:   10
Last:    50
```

---

#### Example 2 — headSet(), tailSet(), subSet()

```java
import java.util.*;

public class TreeSetRange {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(10);
        ts.add(20);
        ts.add(30);
        ts.add(40);
        ts.add(50);

        System.out.println("Full Set:              " + ts);
        System.out.println("headSet(30) — < 30:    " + ts.headSet(30));
        System.out.println("tailSet(30) — >= 30:   " + ts.tailSet(30));
        System.out.println("subSet(20,40) — 20-39: " + ts.subSet(20, 40));
    }
}
```

**Output:**
```
Full Set:              [10, 20, 30, 40, 50]
headSet(30) — < 30:    [10, 20]
tailSet(30) — >= 30:   [30, 40, 50]
subSet(20,40) — 20-39: [20, 30]
```

---

#### Example 3 — String Sorting

```java
import java.util.*;

public class TreeSetString {
    public static void main(String[] args) {

        TreeSet<String> ts = new TreeSet<>();
        ts.add("Banana");
        ts.add("Apple");
        ts.add("Mango");
        ts.add("Cherry");
        ts.add("Apple");   // duplicate

        System.out.println("Sorted Strings: " + ts);
    }
}
```

**Output:**
```
Sorted Strings: [Apple, Banana, Cherry, Mango]
```
> Strings are sorted in **alphabetical (lexicographic)** order.

---

#### Example 4 — Reverse Order using Comparator

```java
import java.util.*;

public class TreeSetReverse {
    public static void main(String[] args) {

        // Descending order
        TreeSet<Integer> ts = new TreeSet<>(Comparator.reverseOrder());
        ts.add(30);
        ts.add(10);
        ts.add(50);
        ts.add(20);
        ts.add(40);

        System.out.println("Descending order: " + ts);
    }
}
```

**Output:**
```
Descending order: [50, 40, 30, 20, 10]
```

---

#### Example 5 — Custom Object Sorting

```java
import java.util.*;

class Student implements Comparable<Student> {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name  = name;
        this.marks = marks;
    }

    // Sort by marks ascending
    public int compareTo(Student s) {
        return this.marks - s.marks;
    }

    public String toString() {
        return name + "(" + marks + ")";
    }
}

public class TreeSetCustom {
    public static void main(String[] args) {

        TreeSet<Student> ts = new TreeSet<>();
        ts.add(new Student("Alice", 85));
        ts.add(new Student("Bob",   72));
        ts.add(new Student("Carol", 91));
        ts.add(new Student("Dave",  68));

        System.out.println("Students by marks: " + ts);
    }
}
```

**Output:**
```
Students by marks: [Dave(68), Bob(72), Alice(85), Carol(91)]
```

---

#### Example 6 — Null Not Allowed in TreeSet

```java
import java.util.*;

public class TreeSetNull {
    public static void main(String[] args) {

        TreeSet<String> ts = new TreeSet<>();
        ts.add("A");
        ts.add("B");
        ts.add(null);   // ❌ throws NullPointerException
    }
}
```

**Output:**
```
Exception in thread "main" java.lang.NullPointerException
```

> TreeSet cannot compare `null` with other elements, so it throws an exception.

---

### Internal Working of TreeSet

TreeSet uses a **Red-Black Tree** internally (a self-balancing binary search tree).

```
Adding: 50, 10, 40, 20, 30

Red-Black Tree:
           30
          /  \
        10    40
          \     \
          20    50

Inorder traversal → 10, 20, 30, 40, 50 (sorted!)
```

Every insertion automatically keeps the tree **balanced and sorted**.

---

## Complete Comparison Table

| Feature | HashSet | LinkedHashSet | TreeSet (SortedSet) |
|---------|---------|---------------|---------------------|
| Duplicates | ❌ | ❌ | ❌ |
| Insertion Order | ❌ Random | ✅ Maintained | ❌ |
| Sorting | ❌ | ❌ | ✅ Ascending |
| Null allowed | ✅ One null | ✅ One null | ❌ |
| Thread safe | ❌ | ❌ | ❌ |
| Speed (add/search) | Fastest O(1) | Fast O(1) | Slower O(log n) |
| Internal structure | HashMap | LinkedHashMap | Red-Black Tree |
| Java version | 1.2 | 1.4 | 1.2 |
| Extra methods | None | None | first(), last(), headSet(), tailSet(), subSet() |
| Use when | Order doesn't matter, fast access | Insertion order matters | Sorted data needed |

---

## When to Use Which?

```
Need a Set (no duplicates)?
        │
        ├── Do you need sorting?
        │         └── YES → Use TreeSet
        │
        ├── Do you need insertion order?
        │         └── YES → Use LinkedHashSet
        │
        └── Neither order nor sorting matters?
                    └── Use HashSet (fastest)
```

---

## Important Rules to Remember

1. **HashSet, LinkedHashSet** — allow **one null**
2. **TreeSet** — does **NOT allow null** (NullPointerException)
3. **TreeSet** — elements must be **Comparable** or provide a **Comparator**
4. **HashSet** is the **fastest** because it uses hashing O(1)
5. **TreeSet** is **slower** because it uses tree structure O(log n)
6. All three are **not thread-safe** — use `Collections.synchronizedSet()` if needed
7. **LinkedHashSet** is the best choice for removing duplicates while keeping order

---

## Thread Safety (Synchronized Set)

If multiple threads use the same Set, make it thread-safe:

```java
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
```

---

## Interview Questions

**Q1. What is the difference between HashSet, LinkedHashSet, and TreeSet?**
HashSet stores in random order, LinkedHashSet maintains insertion order, TreeSet sorts elements. All three reject duplicates.

**Q2. Can we store null in a Set?**
HashSet and LinkedHashSet allow one null. TreeSet does NOT allow null — it throws NullPointerException.

**Q3. Which Set is the fastest?**
HashSet is the fastest because it uses hashing (O(1) time complexity).

**Q4. How does HashSet check for duplicates?**
It uses `hashCode()` to find the bucket and `equals()` to check if the same element exists.

**Q5. Why does TreeSet not allow null?**
TreeSet uses `compareTo()` to sort elements. Comparing null with any object throws NullPointerException.

**Q6. What is the difference between SortedSet and TreeSet?**
SortedSet is an interface. TreeSet is the implementation class of SortedSet.

**Q7. How do you sort custom objects in TreeSet?**
The class must implement the `Comparable` interface and override `compareTo()`, or pass a `Comparator` to the TreeSet constructor.

**Q8. What is the internal data structure of each Set?**
- HashSet → HashMap
- LinkedHashSet → LinkedHashMap
- TreeSet → Red-Black Tree

**Q9. What is the default sorting order in TreeSet?**
Ascending (natural order). For descending, pass `Comparator.reverseOrder()`.

**Q10. What is the time complexity of add and search in each Set?**
- HashSet → O(1)
- LinkedHashSet → O(1)
- TreeSet → O(log n)

---

*Notes compiled for Core Java — Collection Framework*

# Java TreeSet — Complete Notes

> **Topic:** Java Collection Framework — TreeSet
> **Subject:** Core Java

---

## What is TreeSet?

**TreeSet** is a class in Java that stores elements in **sorted order automatically**.

Think of it like a **self-sorting box** — whenever you put something in, it automatically arranges itself from smallest to largest.

It implements the **SortedSet** and **NavigableSet** interfaces.

```
Collection
    └── Set
            └── SortedSet
                    └── NavigableSet
                            └── TreeSet  ← We are here
```

---

## Key Properties of TreeSet

| Property | Value |
|----------|-------|
| Duplicates | ❌ Not allowed |
| Insertion Order | ❌ Not maintained |
| Sorting | ✅ Ascending (natural order by default) |
| Null values | ❌ Not allowed — throws `NullPointerException` |
| Thread Safe | ❌ No |
| Internal Structure | **Red-Black Tree** (self-balancing BST) |
| Time Complexity | O(log n) for add, remove, search |
| Introduced in | Java 1.2 |
| Package | `java.util` |

---

## How to Create a TreeSet

```java
import java.util.TreeSet;

// 1. Default — natural ascending order
TreeSet<Integer> ts = new TreeSet<>();

// 2. Descending order using Comparator
TreeSet<Integer> ts = new TreeSet<>(Comparator.reverseOrder());

// 3. Custom Comparator
TreeSet<String> ts = new TreeSet<>((a, b) -> b.compareTo(a));

// 4. From another Collection
List<Integer> list = Arrays.asList(5, 3, 1, 4, 2);
TreeSet<Integer> ts = new TreeSet<>(list);
```

---

## All Methods of TreeSet

TreeSet has methods from 3 sources:
1. **Collection interface** — basic methods
2. **SortedSet interface** — range methods
3. **NavigableSet interface** — navigation methods

### Basic Methods (from Collection/Set)

| Method | What it does |
|--------|-------------|
| `add(Object o)` | Adds element in sorted position |
| `remove(Object o)` | Removes the element |
| `contains(Object o)` | Returns `true` if element exists |
| `size()` | Returns number of elements |
| `isEmpty()` | Returns `true` if empty |
| `clear()` | Removes all elements |
| `iterator()` | Returns Iterator (ascending order) |
| `toArray()` | Converts to Object array |
| `addAll(Collection c)` | Adds all elements from collection |
| `removeAll(Collection c)` | Removes all matching elements |
| `retainAll(Collection c)` | Keeps only matching elements |
| `containsAll(Collection c)` | Returns `true` if all elements exist |

---

### SortedSet Methods (Range Operations)

| Method | What it does |
|--------|-------------|
| `first()` | Returns the **smallest** element |
| `last()` | Returns the **largest** element |
| `headSet(E toElement)` | Returns elements **strictly less than** `toElement` |
| `tailSet(E fromElement)` | Returns elements **greater than or equal to** `fromElement` |
| `subSet(E from, E to)` | Returns elements from `from` (inclusive) to `to` (exclusive) |
| `comparator()` | Returns Comparator used, or `null` if natural order |

---

### NavigableSet Methods (Extra Navigation)

| Method | What it does |
|--------|-------------|
| `lower(E e)` | Returns largest element **strictly less than** `e` |
| `floor(E e)` | Returns largest element **less than or equal to** `e` |
| `higher(E e)` | Returns smallest element **strictly greater than** `e` |
| `ceiling(E e)` | Returns smallest element **greater than or equal to** `e` |
| `pollFirst()` | Removes and returns the **smallest** element |
| `pollLast()` | Removes and returns the **largest** element |
| `descendingSet()` | Returns the set in **reverse (descending)** order |
| `descendingIterator()` | Returns Iterator in **descending** order |
| `headSet(E e, boolean inclusive)` | headSet with option to include/exclude boundary |
| `tailSet(E e, boolean inclusive)` | tailSet with option to include/exclude boundary |
| `subSet(E from, boolean fromInc, E to, boolean toInc)` | subSet with full control |

---

## Examples

### Example 1 — Basic Add and Sorting

```java
import java.util.*;

public class TreeSetBasic {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();

        ts.add(50);
        ts.add(10);
        ts.add(40);
        ts.add(20);
        ts.add(30);
        ts.add(10);   // duplicate — ignored

        System.out.println("TreeSet:  " + ts);
        System.out.println("Size:     " + ts.size());
        System.out.println("First:    " + ts.first());
        System.out.println("Last:     " + ts.last());
    }
}
```

**Output:**
```
TreeSet:  [10, 20, 30, 40, 50]
Size:     5
First:    10
Last:     50
```

---

### Example 2 — String Sorting (Alphabetical)

```java
import java.util.*;

public class TreeSetString {
    public static void main(String[] args) {

        TreeSet<String> ts = new TreeSet<>();
        ts.add("Banana");
        ts.add("Apple");
        ts.add("Mango");
        ts.add("Cherry");
        ts.add("apple");   // lowercase 'a' — different from "Apple"

        System.out.println("Sorted Strings: " + ts);
        System.out.println("First: " + ts.first());
        System.out.println("Last:  " + ts.last());
    }
}
```

**Output:**
```
Sorted Strings: [Apple, Banana, Cherry, Mango, apple]
First: Apple
Last:  apple
```

> 💡 Uppercase letters come before lowercase in ASCII order. So `"Apple"` comes before `"apple"`.

---

### Example 3 — headSet(), tailSet(), subSet()

```java
import java.util.*;

public class TreeSetRange {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(10);
        ts.add(20);
        ts.add(30);
        ts.add(40);
        ts.add(50);
        ts.add(60);

        System.out.println("Full Set:                   " + ts);

        // headSet — elements strictly LESS than 40
        System.out.println("headSet(40):                " + ts.headSet(40));

        // tailSet — elements GREATER THAN OR EQUAL TO 40
        System.out.println("tailSet(40):                " + ts.tailSet(40));

        // subSet — elements from 20 (inclusive) to 50 (exclusive)
        System.out.println("subSet(20, 50):             " + ts.subSet(20, 50));

        // subSet — both inclusive
        System.out.println("subSet(20,true,50,true):    " + ts.subSet(20, true, 50, true));

        // subSet — both exclusive
        System.out.println("subSet(20,false,50,false):  " + ts.subSet(20, false, 50, false));
    }
}
```

**Output:**
```
Full Set:                   [10, 20, 30, 40, 50, 60]
headSet(40):                [10, 20, 30]
tailSet(40):                [40, 50, 60]
subSet(20, 50):             [20, 30, 40]
subSet(20,true,50,true):    [20, 30, 40, 50]
subSet(20,false,50,false):  [30, 40]
```

---

### Example 4 — NavigableSet Methods

```java
import java.util.*;

public class TreeSetNavigable {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(10);
        ts.add(20);
        ts.add(30);
        ts.add(40);
        ts.add(50);

        System.out.println("Set: " + ts);

        // lower  — strictly less than 30
        System.out.println("lower(30):   " + ts.lower(30));   // 20

        // floor  — less than or equal to 30
        System.out.println("floor(30):   " + ts.floor(30));   // 30

        // higher — strictly greater than 30
        System.out.println("higher(30):  " + ts.higher(30));  // 40

        // ceiling — greater than or equal to 30
        System.out.println("ceiling(30): " + ts.ceiling(30)); // 30

        // pollFirst — remove and return smallest
        System.out.println("pollFirst(): " + ts.pollFirst()); // 10
        System.out.println("After pollFirst: " + ts);

        // pollLast — remove and return largest
        System.out.println("pollLast():  " + ts.pollLast());  // 50
        System.out.println("After pollLast:  " + ts);
    }
}
```

**Output:**
```
Set: [10, 20, 30, 40, 50]
lower(30):   20
floor(30):   30
higher(30):  40
ceiling(30): 30
pollFirst(): 10
After pollFirst: [20, 30, 40, 50]
pollLast():  50
After pollLast:  [20, 30, 40]
```

---

### Example 5 — Descending Order

```java
import java.util.*;

public class TreeSetDescending {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(30);
        ts.add(10);
        ts.add(50);
        ts.add(20);
        ts.add(40);

        System.out.println("Ascending:  " + ts);

        // Method 1 — descendingSet()
        System.out.println("Descending: " + ts.descendingSet());

        // Method 2 — Comparator.reverseOrder()
        TreeSet<Integer> tsDesc = new TreeSet<>(Comparator.reverseOrder());
        tsDesc.addAll(ts);
        System.out.println("Reverse TS: " + tsDesc);

        // Method 3 — descendingIterator()
        System.out.print("Desc Iterator: ");
        Iterator<Integer> descItr = ts.descendingIterator();
        while (descItr.hasNext()) {
            System.out.print(descItr.next() + " ");
        }
    }
}
```

**Output:**
```
Ascending:     [10, 20, 30, 40, 50]
Descending:    [50, 40, 30, 20, 10]
Reverse TS:    [50, 40, 30, 20, 10]
Desc Iterator: 50 40 30 20 10
```

---

### Example 6 — Null Not Allowed

```java
import java.util.*;

public class TreeSetNull {
    public static void main(String[] args) {

        TreeSet<String> ts = new TreeSet<>();
        ts.add("A");
        ts.add("B");

        try {
            ts.add(null);  // throws NullPointerException
        } catch (NullPointerException e) {
            System.out.println("Error: Cannot add null to TreeSet!");
        }

        System.out.println("TreeSet: " + ts);
    }
}
```

**Output:**
```
Error: Cannot add null to TreeSet!
TreeSet: [A, B]
```

---

### Example 7 — Custom Object with Comparable

```java
import java.util.*;

class Employee implements Comparable<Employee> {
    int id;
    String name;
    double salary;

    Employee(int id, String name, double salary) {
        this.id     = id;
        this.name   = name;
        this.salary = salary;
    }

    // Sort by salary ascending
    public int compareTo(Employee e) {
        if (this.salary < e.salary) return -1;
        if (this.salary > e.salary) return  1;
        return 0;
    }

    public String toString() {
        return name + "(₹" + salary + ")";
    }
}

public class TreeSetComparable {
    public static void main(String[] args) {

        TreeSet<Employee> ts = new TreeSet<>();
        ts.add(new Employee(1, "Alice",  75000));
        ts.add(new Employee(2, "Bob",    55000));
        ts.add(new Employee(3, "Carol",  90000));
        ts.add(new Employee(4, "Dave",   65000));

        System.out.println("Employees by Salary:");
        for (Employee e : ts) {
            System.out.println("  " + e);
        }

        System.out.println("Lowest Paid:  " + ts.first());
        System.out.println("Highest Paid: " + ts.last());
    }
}
```

**Output:**
```
Employees by Salary:
  Bob(₹55000.0)
  Dave(₹65000.0)
  Alice(₹75000.0)
  Carol(₹90000.0)
Lowest Paid:  Bob(₹55000.0)
Highest Paid: Carol(₹90000.0)
```

---

### Example 8 — Custom Object with Comparator

```java
import java.util.*;

class Student {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name  = name;
        this.marks = marks;
    }

    public String toString() {
        return name + "(" + marks + ")";
    }
}

public class TreeSetComparator {
    public static void main(String[] args) {

        // Sort by name alphabetically
        TreeSet<Student> byName = new TreeSet<>(
            (s1, s2) -> s1.name.compareTo(s2.name)
        );
        byName.add(new Student("Zara",  85));
        byName.add(new Student("Alice", 72));
        byName.add(new Student("Mike",  91));

        System.out.println("By Name:  " + byName);

        // Sort by marks descending
        TreeSet<Student> byMarks = new TreeSet<>(
            (s1, s2) -> s2.marks - s1.marks
        );
        byMarks.add(new Student("Zara",  85));
        byMarks.add(new Student("Alice", 72));
        byMarks.add(new Student("Mike",  91));

        System.out.println("By Marks (desc): " + byMarks);
    }
}
```

**Output:**
```
By Name:         [Alice(72), Mike(91), Zara(85)]
By Marks (desc): [Mike(91), Zara(85), Alice(72)]
```

---

### Example 9 — Iterating TreeSet

```java
import java.util.*;

public class TreeSetIterate {
    public static void main(String[] args) {

        TreeSet<String> ts = new TreeSet<>();
        ts.add("Mango");
        ts.add("Apple");
        ts.add("Banana");
        ts.add("Cherry");

        // Method 1 — for-each (ascending)
        System.out.println("for-each (ascending):");
        for (String s : ts) {
            System.out.print(s + " ");
        }

        // Method 2 — Iterator (ascending)
        System.out.println("\nIterator (ascending):");
        Iterator<String> itr = ts.iterator();
        while (itr.hasNext()) {
            System.out.print(itr.next() + " ");
        }

        // Method 3 — descendingIterator
        System.out.println("\nDescending Iterator:");
        Iterator<String> dItr = ts.descendingIterator();
        while (dItr.hasNext()) {
            System.out.print(dItr.next() + " ");
        }
    }
}
```

**Output:**
```
for-each (ascending):
Apple Banana Cherry Mango
Iterator (ascending):
Apple Banana Cherry Mango
Descending Iterator:
Mango Cherry Banana Apple
```

---

### Example 10 — contains(), remove(), size()

```java
import java.util.*;

public class TreeSetOperations {
    public static void main(String[] args) {

        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(100);
        ts.add(200);
        ts.add(300);
        ts.add(400);
        ts.add(500);

        System.out.println("Set:            " + ts);
        System.out.println("Size:           " + ts.size());
        System.out.println("Contains 300?   " + ts.contains(300));
        System.out.println("Contains 999?   " + ts.contains(999));

        ts.remove(300);
        System.out.println("After remove:   " + ts);

        ts.clear();
        System.out.println("After clear:    " + ts);
        System.out.println("isEmpty?        " + ts.isEmpty());
    }
}
```

**Output:**
```
Set:            [100, 200, 300, 400, 500]
Size:           5
Contains 300?   true
Contains 999?   false
After remove:   [100, 200, 400, 500]
After clear:    []
isEmpty?        true
```

---

## Internal Working — Red-Black Tree

TreeSet uses a **Red-Black Tree** internally (which is a self-balancing Binary Search Tree).

### Rules of Red-Black Tree:
1. Every node is either **Red** or **Black**
2. Root is always **Black**
3. No two consecutive **Red** nodes
4. Every path from root to null has the same number of **Black** nodes

### How Insertion Works:

```
Insert: 30, 10, 50, 20, 40

Step 1 — Insert 30:
        30(B)

Step 2 — Insert 10:
        30(B)
       /
     10(R)

Step 3 — Insert 50:
        30(B)
       /    \
     10(R)  50(R)

Step 4 — Insert 20:
        30(B)
       /    \
     10(B)  50(B)
       \
       20(R)

Step 5 — Insert 40:
        30(B)
       /    \
     10(B)  50(B)
       \    /
      20(R) 40(R)

Inorder traversal → 10, 20, 30, 40, 50 (always sorted!)
```

> 💡 The tree **auto-balances** itself so that searching, inserting, and deleting always takes **O(log n)** time.

---

## Comparable vs Comparator in TreeSet

### Comparable (Natural Ordering)
- The **class itself** defines the sort order
- Override `compareTo()` method
- One fixed sort order

```java
class Book implements Comparable<Book> {
    String title;
    int pages;

    Book(String title, int pages) {
        this.title = title;
        this.pages = pages;
    }

    // Sort by pages ascending
    public int compareTo(Book b) {
        return this.pages - b.pages;
    }
}
```

### Comparator (Custom Ordering)
- Sort order is defined **outside the class**
- Can have **multiple sort orders**
- Passed to TreeSet constructor

```java
// Sort by title
Comparator<Book> byTitle = (b1, b2) -> b1.title.compareTo(b2.title);
TreeSet<Book> ts = new TreeSet<>(byTitle);

// Sort by pages descending
Comparator<Book> byPagesDesc = (b1, b2) -> b2.pages - b1.pages;
TreeSet<Book> ts2 = new TreeSet<>(byPagesDesc);
```

### compareTo() Return Values

| Return Value | Meaning |
|-------------|---------|
| **Negative** (e.g. -1) | Current object is **smaller** — goes first |
| **Zero** (0) | Both objects are **equal** — treated as duplicate |
| **Positive** (e.g. +1) | Current object is **larger** — goes after |

---

## Limitations of TreeSet

1. **No null allowed** — throws NullPointerException
2. **Slower than HashSet** — O(log n) vs O(1)
3. **Thread unsafe** — need external synchronization
4. **Custom objects must implement Comparable** or pass a Comparator — else `ClassCastException`
5. **Only one sort order** per TreeSet instance

---

## TreeSet vs HashSet vs LinkedHashSet

| Feature | TreeSet | HashSet | LinkedHashSet |
|---------|---------|---------|---------------|
| Order | Sorted | Random | Insertion order |
| Null | ❌ No | ✅ One | ✅ One |
| Speed | O(log n) | O(1) | O(1) |
| Duplicates | ❌ | ❌ | ❌ |
| Internal | Red-Black Tree | HashMap | LinkedHashMap |
| Extra methods | first, last, headSet, etc. | None | None |
| Best for | Sorted data | Fast access | Ordered access |

---

## Common Mistakes to Avoid

```java
// ❌ Adding null
ts.add(null);  // NullPointerException

// ❌ Custom object without Comparable or Comparator
TreeSet<Dog> ts = new TreeSet<>();
ts.add(new Dog("Tommy"));  // ClassCastException at runtime

// ✅ Correct — implement Comparable
class Dog implements Comparable<Dog> {
    public int compareTo(Dog d) {
        return this.name.compareTo(d.name);
    }
}

// ❌ Expecting insertion order
TreeSet<Integer> ts = new TreeSet<>();
ts.add(3); ts.add(1); ts.add(2);
System.out.println(ts);  // prints [1, 2, 3] not [3, 1, 2]
```

---

## Thread Safety

TreeSet is **not thread-safe** by default. To make it thread-safe:

```java
Set<Integer> syncTreeSet = Collections.synchronizedSortedSet(new TreeSet<>());
```

---

## Interview Questions

**Q1. What is TreeSet in Java?**
TreeSet is a class that implements SortedSet and NavigableSet interfaces. It stores elements in sorted ascending order using a Red-Black Tree internally.

**Q2. What is the internal data structure of TreeSet?**
Red-Black Tree — a self-balancing binary search tree.

**Q3. What is the time complexity of TreeSet operations?**
All major operations (add, remove, contains) take O(log n) time.

**Q4. Why does TreeSet not allow null?**
TreeSet uses compareTo() to sort elements. Comparing null with any object throws NullPointerException.

**Q5. What happens if we add a custom object to TreeSet without implementing Comparable?**
It throws ClassCastException at runtime.

**Q6. What is the difference between Comparable and Comparator in TreeSet?**
Comparable is implemented by the class itself for natural ordering. Comparator is passed externally to TreeSet for custom ordering. You can have multiple Comparators but only one Comparable.

**Q7. What is the difference between lower() and floor()?**
`lower(e)` returns the largest element strictly less than e. `floor(e)` returns the largest element less than or equal to e.

**Q8. What is the difference between headSet(), tailSet(), and subSet()?**
`headSet(e)` returns elements less than e. `tailSet(e)` returns elements >= e. `subSet(from, to)` returns elements from (inclusive) to to (exclusive).

**Q9. What does pollFirst() and pollLast() do?**
`pollFirst()` removes and returns the smallest element. `pollLast()` removes and returns the largest element. Both return null if the set is empty.

**Q10. How do you iterate TreeSet in descending order?**
Use `ts.descendingSet()` or `ts.descendingIterator()`.

**Q11. How do you make TreeSet thread-safe?**
Use `Collections.synchronizedSortedSet(new TreeSet<>())`.

**Q12. Can TreeSet contain duplicate elements?**
No. TreeSet rejects duplicates. If compareTo() returns 0, the element is treated as a duplicate and not added.

---

*Notes compiled for Core Java — Collection Framework*