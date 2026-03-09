# Three Cursors of Java - Enumeration

* Introduced in 1.0 version (for Legacy).
* We can use Enumeration to get Objects one by one from the old Collection Objects (Legacy Collections).
* We can create an Enumeration Object by using the elements() method of the Vector class.

**Method Signature:**
```
public Enumeration elements();
```
**Example:**
```
Enumeration e = v.elements();
```
------------------------------

💡 **Quick Insight:**  
Enumeration is considered a "legacy cursor." While it works for traversing Vector and Stack, it has two main limitations compared to the modern Iterator:

1. It is read-only (it doesn't have a remove() method).
2. The method names are quite long (hasMoreElements() vs hasNext()).

Would you like to see the comparison table between Enumeration, Iterator, and ListIterator to see which one is best for your specific use case?
## Example Code

```java
import java.util.*;

class EnumaretionDemo1 {
    public static void main(String arg[]) {
        Vector v = new Vector();
        
        for (int i = 0; i <= 10; i++) {
            v.addElement(i);
        }
        System.out.println(v); // [0,1,2,3,4,5....10]

        Enumeration e = v.elements();
        while (e.hasMoreElements()) {
            Integer i = (Integer) e.nextElement();
            if ((i % 2) == 0) {
                System.out.println(i); // [0 2 4 6 8 10]
            }
        }
        System.out.println(v); // [0,1,2,3,4,5,...10]
    }
}
```

**Output:**
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
0
2
4
6
8
10
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

# Java Three Cursors — Iterator & ListIterator

> **Topic:** Java Collection Framework — Cursors
> **Subject:** Core Java

---

## What is a Cursor?

A **cursor** is an object that helps you **traverse (loop through)** a collection one element at a time.

Java provides **3 types of cursors:**

| # | Cursor | Works With | Can Remove? | Can Go Backward? | Can Replace? |
|---|--------|-----------|-------------|------------------|--------------|
| 1 | Enumeration | Legacy (Vector, Stack) | ❌ No | ❌ No | ❌ No |
| 2 | Iterator | All Collections | ✅ Yes | ❌ No | ❌ No |
| 3 | ListIterator | Only List | ✅ Yes | ✅ Yes | ✅ Yes |

---

## 1. Enumeration (Legacy Cursor)

- The **oldest** cursor in Java (since Java 1.0)
- Works only with **legacy classes** like `Vector`, `Stack`, `Hashtable`
- **Read-only** — cannot remove elements
- **Forward-only** — cannot go backward

```java
Vector<String> v = new Vector<>();
v.add("A");
v.add("B");

Enumeration<String> e = v.elements();
while (e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

### Methods of Enumeration

| Method | What it does |
|--------|-------------|
| `hasMoreElements()` | Returns `true` if more elements exist |
| `nextElement()` | Returns the next element |

> ⚠️ **Limitation:** Only works with legacy classes. Cannot remove elements. Forward direction only.

---

## 2. Iterator (Universal Cursor)

- Introduced in **Java 1.2**
- Works with **any Collection** — List, Set, Queue, etc.
- That is why it is called a **Universal Cursor**
- Can **read and remove** elements during iteration
- **Forward-only** — cannot go backward

### How to Create an Iterator

```java
Iterator itr = C.iterator();
```

Where `C` is any Collection object.

### Example

```java
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Mango");

Iterator<String> itr = list.iterator();

while (itr.hasNext()) {
    String item = itr.next();
    System.out.println(item);   // Apple, Banana, Mango
}
```

### Methods of Iterator

| Method | Signature | What it does |
|--------|-----------|-------------|
| `hasNext()` | `public boolean hasNext()` | Returns `true` if next element exists |
| `next()` | `public Object next()` | Moves forward and returns the element |
| `remove()` | `public void remove()` | Removes the current element |

### Remove Example

```java
Iterator<Integer> itr = list.iterator();
while (itr.hasNext()) {
    int val = itr.next();
    if (val % 2 == 0) {
        itr.remove();  // removes even numbers safely
    }
}
```

> ⚠️ Never use `list.remove()` inside an iterator loop — it causes `ConcurrentModificationException`. Always use `itr.remove()`.

---

## Limitations of Iterator

1. **Single Direction** — Can only move **forward**. Cannot go backward.
2. **Limited Operations** — Can only **read** and **remove**. Cannot **add** or **replace** elements.

> 💡 To overcome these limitations, use **ListIterator**.

---

## 3. ListIterator (Most Powerful Cursor)

- Works only with **List** classes (`ArrayList`, `LinkedList`, `Vector`)
- Can move **forward and backward** — Bidirectional
- Can **read, remove, add, and replace** elements
- Extends the `Iterator` interface

### How to Create a ListIterator

```java
ListIterator litr = L.listIterator();
```

Where `L` is any List object.

### Example

```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

ListIterator<String> litr = list.listIterator();

// Forward traversal
while (litr.hasNext()) {
    System.out.println(litr.next());  // A, B, C
}

// Backward traversal
while (litr.hasPrevious()) {
    System.out.println(litr.previous());  // C, B, A
}
```

### Methods of ListIterator

| Method | What it does |
|--------|-------------|
| `hasNext()` | Returns `true` if next element exists (forward) |
| `next()` | Returns next element and moves forward |
| `hasPrevious()` | Returns `true` if previous element exists (backward) |
| `previous()` | Returns previous element and moves backward |
| `remove()` | Removes current element |
| `set(Object o)` | **Replaces** current element with new one |
| `add(Object o)` | **Adds** a new element at current position |
| `nextIndex()` | Returns index of the next element |
| `previousIndex()` | Returns index of the previous element |

### Replace Element Example

```java
ListIterator<String> litr = list.listIterator();
while (litr.hasNext()) {
    String val = litr.next();
    if (val.equals("B")) {
        litr.set("Z");  // replaces B with Z
    }
}
// list is now [A, Z, C]
```

---

## Quick Comparison Summary

| Feature | Enumeration | Iterator | ListIterator |
|---------|------------|----------|--------------|
| Works with | Legacy only | All Collections | List only |
| Forward traversal | ✅ | ✅ | ✅ |
| Backward traversal | ❌ | ❌ | ✅ |
| Remove element | ❌ | ✅ | ✅ |
| Add element | ❌ | ❌ | ✅ |
| Replace element | ❌ | ❌ | ✅ |
| Since Java version | 1.0 | 1.2 | 1.2 |

---

## Key Rules to Remember

- Always use `itr.remove()` — never `collection.remove()` inside a loop
- `ListIterator` only works with **List** — not Set or Queue
- `Iterator` is enough when you just need to **read or delete**
- Use `ListIterator` when you need to **replace or go backward**
- `Enumeration` is **outdated** — avoid using it in new code

---

## Interview Questions

**Q1. Why is Iterator called a Universal Cursor?**
Because it works with any Collection (List, Set, Queue), unlike Enumeration which only works with legacy classes.

**Q2. What happens if you call `next()` without checking `hasNext()`?**
It throws `NoSuchElementException`.

**Q3. What is the difference between Iterator and ListIterator?**
Iterator is forward-only and works with all collections. ListIterator is bidirectional but works only with List.

**Q4. Can we add elements using Iterator?**
No. Only ListIterator supports adding elements using `add()`.

---

*Notes compiled for Core Java — Collection Framework*

# Java ListIterator — Complete Notes

> **Topic:** Java Collection Framework — ListIterator
> **Subject:** Core Java

---

## What is ListIterator?

**ListIterator** is the most powerful cursor in Java.

Think of it like a **two-way train** — it can go **forward AND backward**, and it can also **add, remove, and replace** elements while traveling.

It is a **child interface** of `Iterator`, which means it has all the methods of Iterator **plus** extra methods of its own.

---

## Why ListIterator?

Iterator had 2 big limitations:
1. Could only go **forward**
2. Could only **read and remove** — not add or replace

ListIterator **solves both** of these problems.

---

## Where Can We Use ListIterator?

> ⚠️ **Important:** ListIterator works **only with List** classes.

It does **NOT** work with Set or Queue.

| Collection | ListIterator Works? |
|------------|-------------------|
| `ArrayList` | ✅ Yes |
| `LinkedList` | ✅ Yes |
| `Vector` | ✅ Yes |
| `HashSet` | ❌ No |
| `TreeSet` | ❌ No |
| `PriorityQueue` | ❌ No |

---

## How to Create a ListIterator

```java
ListIterator litr = L.listIterator();
```

Where `L` is any **List** object.

**Method Signature:**
```java
public ListIterator listIterator();
```

**Full Example:**
```java
List<String> list = new ArrayList<>();
ListIterator<String> litr = list.listIterator();
```

---

## All 9 Methods of ListIterator

ListIterator has **9 methods** in total.

### Forward Direction Methods

| Method | Signature | What it does |
|--------|-----------|-------------|
| `hasNext()` | `public boolean hasNext()` | Returns `true` if next element exists |
| `next()` | `public Object next()` | Returns next element and moves forward |
| `nextIndex()` | `public int nextIndex()` | Returns **index** of the next element |

### Backward Direction Methods

| Method | Signature | What it does |
|--------|-----------|-------------|
| `hasPrevious()` | `public boolean hasPrevious()` | Returns `true` if previous element exists |
| `previous()` | `public Object previous()` | Returns previous element and moves backward |
| `previousIndex()` | `public int previousIndex()` | Returns **index** of the previous element |

### Modification Methods

| Method | Signature | What it does |
|--------|-----------|-------------|
| `remove()` | `public void remove()` | Removes the **current** element |
| `set(Object o)` | `public void set(Object o)` | **Replaces** current element with new one |
| `add(Object o)` | `public void add(Object o)` | **Adds** new element at current position |

---

## Examples

### Example 1 — Forward Traversal

```java
import java.util.*;

public class ListIteratorForward {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Mango");
        list.add("Orange");

        // Create ListIterator
        ListIterator<String> litr = list.listIterator();

        System.out.println("Forward Traversal:");
        while (litr.hasNext()) {
            String item = litr.next();
            System.out.println(item);
        }
    }
}
```

**Output:**
```
Forward Traversal:
Apple
Banana
Mango
Orange
```

---

### Example 2 — Backward Traversal

```java
import java.util.*;

public class ListIteratorBackward {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Mango");
        list.add("Orange");

        ListIterator<String> litr = list.listIterator();

        // First go to the end using forward loop
        while (litr.hasNext()) {
            litr.next();
        }

        // Now go backward
        System.out.println("Backward Traversal:");
        while (litr.hasPrevious()) {
            String item = litr.previous();
            System.out.println(item);
        }
    }
}
```

**Output:**
```
Backward Traversal:
Orange
Mango
Banana
Apple
```

---

### Example 3 — Both Forward and Backward in One Program

```java
import java.util.*;

public class ListIteratorBothWays {
    public static void main(String[] args) {

        List<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        list.add(40);
        list.add(50);

        ListIterator<Integer> litr = list.listIterator();

        // Forward
        System.out.println("=== Forward ===");
        while (litr.hasNext()) {
            System.out.println(litr.next());
        }

        // Backward (cursor is now at end, so we go back)
        System.out.println("=== Backward ===");
        while (litr.hasPrevious()) {
            System.out.println(litr.previous());
        }
    }
}
```

**Output:**
```
=== Forward ===
10
20
30
40
50
=== Backward ===
50
40
30
20
10
```

---

### Example 4 — Replace Elements using `set()`

```java
import java.util.*;

public class ListIteratorSet {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        list.add("cat");
        list.add("dog");
        list.add("bird");

        System.out.println("Before: " + list);

        ListIterator<String> litr = list.listIterator();

        while (litr.hasNext()) {
            String item = litr.next();
            // Replace every element with its UPPERCASE version
            litr.set(item.toUpperCase());
        }

        System.out.println("After:  " + list);
    }
}
```

**Output:**
```
Before: [cat, dog, bird]
After:  [CAT, DOG, BIRD]
```

---

### Example 5 — Add Elements using `add()`

```java
import java.util.*;

public class ListIteratorAdd {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");

        System.out.println("Before: " + list);

        ListIterator<String> litr = list.listIterator();

        while (litr.hasNext()) {
            String item = litr.next();
            // Add a "*" after every element
            litr.add(item + "*");
        }

        System.out.println("After:  " + list);
    }
}
```

**Output:**
```
Before: [A, B, C]
After:  [A, A*, B, B*, C, C*]
```

---

### Example 6 — Remove Elements using `remove()`

```java
import java.util.*;

public class ListIteratorRemove {
    public static void main(String[] args) {

        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);
        list.add(6);

        System.out.println("Before: " + list);

        ListIterator<Integer> litr = list.listIterator();

        while (litr.hasNext()) {
            int val = litr.next();
            // Remove all even numbers
            if (val % 2 == 0) {
                litr.remove();
            }
        }

        System.out.println("After:  " + list);
    }
}
```

**Output:**
```
Before: [1, 2, 3, 4, 5, 6]
After:  [1, 3, 5]
```

---

### Example 7 — Using `nextIndex()` and `previousIndex()`

```java
import java.util.*;

public class ListIteratorIndex {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        list.add("Red");
        list.add("Green");
        list.add("Blue");

        ListIterator<String> litr = list.listIterator();

        while (litr.hasNext()) {
            System.out.println(
                "Next Index: " + litr.nextIndex() +
                " | Element: " + litr.next() +
                " | Prev Index: " + litr.previousIndex()
            );
        }
    }
}
```

**Output:**
```
Next Index: 0 | Element: Red   | Prev Index: -1
Next Index: 1 | Element: Green | Prev Index: 0
Next Index: 2 | Element: Blue  | Prev Index: 1
```

> 💡 When the cursor is at the **start**, `previousIndex()` returns `-1` because there is no previous element.

---

## ListIterator vs Iterator — Full Comparison

| Feature | Iterator | ListIterator |
|---------|----------|--------------|
| Works with | All Collections | List only |
| Forward traversal | ✅ | ✅ |
| Backward traversal | ❌ | ✅ |
| Read element | ✅ `next()` | ✅ `next()` / `previous()` |
| Remove element | ✅ `remove()` | ✅ `remove()` |
| Replace element | ❌ | ✅ `set()` |
| Add element | ❌ | ✅ `add()` |
| Get index | ❌ | ✅ `nextIndex()` / `previousIndex()` |
| Total methods | 3 | 9 |
| Interface extends | `Iterable` | `Iterator` |

---

## Internal Working — How the Cursor Moves

```
List:  [ A ]  [ B ]  [ C ]  [ D ]
Index:   0      1      2      3

Cursor positions (between elements):
^         ^         ^         ^         ^
Start    Pos1     Pos2     Pos3      End

- next()     moves cursor one step RIGHT
- previous() moves cursor one step LEFT
```

The cursor sits **between** elements, not on them. That is why `nextIndex()` and `previousIndex()` can return different values at the same position.

---

## Important Rules and Tips

1. **Always call `next()` or `previous()` before calling `set()` or `remove()`** — otherwise you get `IllegalStateException`

2. **Cannot call `remove()` and `set()` together** without calling `next()` or `previous()` again in between

3. **`add()` inserts at the current cursor position** — it does not replace

4. **ListIterator works only on List** — trying it on Set or Queue gives a compile error

5. **`previousIndex()` returns `-1`** when cursor is at the very beginning

6. **`nextIndex()` returns `list.size()`** when cursor is at the very end

---

## Common Mistakes to Avoid

```java
// ❌ WRONG — calling set() without next() first
ListIterator<String> litr = list.listIterator();
litr.set("X");  // throws IllegalStateException

// ✅ CORRECT
litr.next();
litr.set("X");  // works fine
```

```java
// ❌ WRONG — calling remove() twice in a row
litr.next();
litr.remove();
litr.remove();  // throws IllegalStateException

// ✅ CORRECT — must call next() again between removes
litr.next();
litr.remove();
litr.next();
litr.remove();
```

---

## Interview Questions

**Q1. What is ListIterator and how is it different from Iterator?**
ListIterator is a child interface of Iterator that works only with List. It supports bidirectional traversal and allows add, remove, and replace operations. Iterator only supports forward traversal and remove.

**Q2. Can we use ListIterator with a HashSet?**
No. ListIterator works only with List implementations like ArrayList, LinkedList, and Vector.

**Q3. What exception is thrown if we call `set()` without calling `next()` first?**
`IllegalStateException` is thrown.

**Q4. What does `previousIndex()` return when the cursor is at the start?**
It returns `-1` because there is no previous element.

**Q5. What is the difference between `add()` in ListIterator and `add()` in List?**
`litr.add()` inserts at the current cursor position during iteration safely. `list.add()` during iteration causes `ConcurrentModificationException`.

**Q6. How many methods does ListIterator have?**
ListIterator has 9 methods — `hasNext()`, `next()`, `nextIndex()`, `hasPrevious()`, `previous()`, `previousIndex()`, `remove()`, `set()`, and `add()`.

---

*Notes compiled for Core Java — Collection Framework*

### comaresion of three cursors of java
Comparison of the Three Cursors of Java

| Property | Enumeration | Iterator | ListIterator |
|---|---|---|---|
| Applicable for | Only legacy classes | Any Collection classes | Only List classes |
| Movement | Only forward direction (single direction) | Only forward direction (single direction) | Both forward and backward direction (bidirectional) |
| Accessibility | Only read access | Both read and remove | Read, remove, replace and addition of new objects |
| How to get it? | By using elements() method of Vector class | By using iterator() method of Collection interface | By using listIterator() method of List interface |
| Methods | 2 methods: hasMoreElements(), nextElement() | 3 methods: hasNext(), next(), remove() | 9 methods |
| Is it legacy | "yes" (1.0v) | "no" (1.2v) | "no" (1.2v) |

------------------------------
