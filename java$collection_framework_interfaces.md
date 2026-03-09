
# Java Collection Framework Interfaces

## 1. Collection

* If we want to represent a group of individual objects as a single entity, we should use Collection.
* Collection interface defines the most common methods applicable to any Collection object.
* Collection interface is considered the root interface of the Collection Framework.

**Note:** No concrete class directly implements the Collection interface.

### Common Methods
- `add(E e)` - Adds an element
- `remove(Object o)` - Removes an element
- `contains(Object o)` - Checks if element exists
- `size()` - Returns the number of elements
- `isEmpty()` - Checks if collection is empty
- `iterator()` - Returns an iterator

---

## Collection vs Map

| Aspect | Collection | Map |
|--------|-----------|-----|
| Hierarchy | Root interface | Separate interface (not a Collection) |
| Structure | Group of objects | Key-value pairs |
| Duplicates | Allowed in most implementations | Keys must be unique |
| Order | Depends on implementation | Depends on implementation |
| Examples | List, Set, Queue | HashMap, TreeMap, Hashtable |


## Difference between Collection & Collections

| Aspect | Collection | Collections |
|--------|-----------|-------------|
| Type | Interface | Utility class |
| Purpose | Represents a group of objects | Provides utility methods for Collection objects |
| Package | java.util | java.util |
| Usage | Implement to create collections | Use static methods for operations |
| Examples | List, Set, Queue | sort(), search(), reverse(), shuffle() |

**Collection** is an interface used to represent a group of individual objects as a single entity.

**Collections** is a utility class that provides several static utility methods for Collection objects such as sorting, searching, and other operations.
## 2. List

* List is a child interface of Collection.
* If we want to represent a group of individual objects as a single entity where duplicates are allowed and insertion order is preserved, we should use List.

### Characteristics
- Duplicates are allowed
- Insertion order is preserved
- Elements are accessed by index (0-based)
- Allows null elements

### Common Methods
- `add(int index, E e)` - Adds element at specific index
- `get(int index)` - Retrieves element at index
- `remove(int index)` - Removes element at index
- `indexOf(Object o)` - Returns index of element
- `subList(int fromIndex, int toIndex)` - Returns a sub-list

### Common Implementations
- ArrayList
- LinkedList
- Vector
- Stack
## 3. Set

* Set is a child interface of Collection.
* If we want to represent a group of individual objects as a single entity where duplicates are not allowed and insertion order is not preserved, we should use Set.

### Characteristics
- Duplicates are not allowed
- Insertion order is not preserved
- No index-based access
- Allows null elements (in most implementations)

### Common Methods
- `add(E e)` - Adds element if not already present
- `remove(Object o)` - Removes element
- `contains(Object o)` - Checks if element exists
- `iterator()` - Returns an iterator

### Common Implementations
- HashSet
- LinkedHashSet
- TreeSet

### List vs Set

| Aspect | List | Set |
|--------|------|-----|
| Duplicates | Allowed | Not allowed |
| Order | Insertion order preserved | No order guarantee |
| Access | Index-based access | No index-based access |
| Performance | Good for retrieval by index | Good for uniqueness checking |
| Examples | ArrayList, LinkedList | HashSet, TreeSet |

## 4. Queue

* Queue is a child interface of Collection.
* If we want to represent a group of individual objects as a single entity where elements are processed in FIFO (First-In-First-Out) order, we should use Queue.

### Characteristics
- Elements are added at the rear and removed from the front
- Follows FIFO principle
- Duplicates are allowed
- Order is preserved (insertion order)

### Common Methods
- `add(E e)` - Adds element to the queue
- `remove()` - Removes and returns the head element
- `peek()` - Returns the head element without removing
- `poll()` - Removes and returns the head element or null
- `offer(E e)` - Adds element to the queue

### Common Implementations
- LinkedList
- PriorityQueue
- Deque (Double-ended queue)

---

## Summary Table

| Interface | Duplicates | Order | Access | Use Case |
|-----------|-----------|-------|--------|----------|
| List | Allowed | Preserved | Index-based | When order and duplicates matter |
| Set | Not allowed | Not preserved | No index | When uniqueness is required |
| Queue | Allowed | FIFO | Front/Rear | When FIFO processing is needed |

## 5. SortedSet

* SortedSet is a child interface of Set.
* Elements are sorted in ascending order according to their natural ordering or a custom comparator.
* Provides methods to access elements based on their sort order.

### Common Methods
- `first()` - Returns the first (lowest) element
- `last()` - Returns the last (highest) element
- `headSet(E toElement)` - Returns elements less than toElement
- `tailSet(E fromElement)` - Returns elements greater than or equal to fromElement
- `subSet(E fromElement, E toElement)` - Returns elements in range

### Common Implementations
- TreeSet

---

## 6. NavigableSet

* NavigableSet is a child interface of SortedSet.
* Defines several methods for navigation purposes to traverse the set in both directions.

### Common Methods
- `lower(E e)` - Returns the greatest element less than e
- `floor(E e)` - Returns the greatest element less than or equal to e
- `ceiling(E e)` - Returns the least element greater than or equal to e
- `higher(E e)` - Returns the least element greater than e
- `pollFirst()` - Removes and returns the first element
- `pollLast()` - Removes and returns the last element
- `descendingIterator()` - Returns an iterator in descending order

### Common Implementations
- TreeSet

## 7. Map

* Map is a separate interface (not a child of Collection).
* If we want to represent a group of objects as key-value pairs, we should use Map.
* Each key is associated with exactly one value.

### Characteristics
- Keys must be unique
- Values can be duplicated
- Each key maps to exactly one value
- No index-based access
- Allows null keys and values (in most implementations)

### Common Methods
- `put(K key, V value)` - Associates a key with a value
- `get(Object key)` - Returns value for key
- `remove(Object key)` - Removes key-value pair
- `containsKey(Object key)` - Checks if key exists
- `containsValue(Object value)` - Checks if value exists
- `keySet()` - Returns set of keys
- `values()` - Returns collection of values
- `entrySet()` - Returns set of key-value pairs
- `size()` - Returns number of key-value pairs

### Common Implementations
- HashMap
- LinkedHashMap
- TreeMap
- Hashtable
- WeakHashMap
- IdentityHashMap

---

## 8. SortedMap

* SortedMap is a child interface of Map.
* Keys are sorted in ascending order according to their natural ordering or a custom comparator.

### Common Methods
- `firstKey()` - Returns the first (lowest) key
- `lastKey()` - Returns the last (highest) key
- `headMap(K toKey)` - Returns entries with keys less than toKey
- `tailMap(K fromKey)` - Returns entries with keys greater than or equal to fromKey
- `subMap(K fromKey, K toKey)` - Returns entries with keys in range

### Common Implementations
- TreeMap

---

## 9. NavigableMap

* NavigableMap is a child interface of SortedMap.
* Defines several methods for navigation purposes to traverse the map in both directions.

### Common Methods
- `lowerKey(K key)` - Returns the greatest key less than key
- `floorKey(K key)` - Returns the greatest key less than or equal to key
- `ceilingKey(K key)` - Returns the least key greater than or equal to key
- `higherKey(K key)` - Returns the least key greater than key
- `pollFirstEntry()` - Removes and returns the first entry
- `pollLastEntry()` - Removes and returns the last entry
- `descendingMap()` - Returns a reverse-order view of the map

### Common Implementations
- TreeMap

## Key Points

* Map is not a child interface of Collection; it has its own separate hierarchy.
* Map is used to represent a group of objects as key-value pairs.
* Duplicates are not allowed for keys, but values can be duplicated.
* Each key is associated with exactly one value.

### Example

| Roll No (Key) | Name (Value) |
|---|---|
| 101 | Durga |
| 102 | Ravi |
| 103 | Venkat |

In this example, roll numbers are unique keys, and names are values (which could potentially be duplicated across different students).

## 10. Important Methods of Collection Interface

The Collection interface provides various methods for manipulating and querying groups of objects.

### Modification Methods
- `add(Object o)` - Adds an object to the collection
- `addAll(Collection c)` - Adds all elements from another collection
- `remove(Object o)` - Removes a specific object
- `removeAll(Collection c)` - Removes all elements that are also in the specified collection
- `retainAll(Collection c)` - Keeps only the elements that are also in the specified collection
- `clear()` - Removes all elements from the collection

### Query & Utility Methods
- `contains(Object o)` - Checks if a specific object is present
- `containsAll(Collection c)` - Checks if all elements of another collection are present
- `isEmpty()` - Checks if the collection has no elements
- `size()` - Returns the number of elements in the collection
- `toArray()` - Converts the collection into an array of objects
- `iterator()` - Returns an iterator to loop through the elements
