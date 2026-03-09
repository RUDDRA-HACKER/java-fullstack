
# Linked List

## Overview
A linked list is a linear data structure where elements (nodes) are connected via pointers/references rather than contiguous memory locations.

## Node Structure
```java
class Node {
    int data;
    Node next;
    
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

## Common Operations
- **Insert**: Add element at beginning, end, or specific position - O(n)
- **Delete**: Remove element - O(n)
- **Search**: Find element - O(n)
- **Traverse**: Visit all nodes - O(n)

## Advantages
- Dynamic memory allocation
- Easy insertion/deletion
- No wasted memory (in comparison to arrays)

## Disadvantages
- Extra memory for pointers
- No random access
- Cache unfriendly

## Types
- **Singly Linked List**: Each node points to the next
- **Doubly Linked List**: Each node points to next and previous
- **Circular Linked List**: Last node points back to first
import java.util.*;
```java
public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList l1 = new LinkedList();
        
        l1.add("durga");
        l1.add(30);
        l1.add(null);
        l1.add("durga");
        l1.set(0, "software");
        l1.add(0, "venkey");
        l1.addFirst("ccc");
        
        System.out.println(l1); // Output: [ccc, venkey, software, 30, null, durga]
    }
}
```
/**
 * Comparison Documentation: ArrayList vs LinkedList
 * 
 * This document outlines the key differences between ArrayList and LinkedList
 * data structures in Java, including their performance characteristics and
 * underlying implementations.
 * 
 * ## Performance Characteristics
 * - ArrayList: Optimal for frequent retrieval operations
 * - LinkedList: Optimal for frequent insertion and deletion operations
 * 
 * ## Underlying Data Structures
 * - ArrayList: Uses a resizable/growable dynamic array
 * - LinkedList: Uses a doubly-linked list structure
 * 
 * ## Interface Implementations
 * - ArrayList: Implements the RandomAccess interface, enabling O(1) element access
 * - LinkedList: Does not implement RandomAccess, requiring O(n) traversal for access
 * 
 * ## Trade-offs
 * - ArrayList: Poor performance for insertion/deletion operations due to element shifting
 * - LinkedList: Poor performance for retrieval operations due to sequential traversal
 * 
 * @note The RandomAccess interface is a marker interface that indicates
 *       an implementation supports fast (O(1)) random access to elements,
 *       which is a key advantage of ArrayList over LinkedList.
 */
/**
 * Comparison between ArrayList and LinkedList
 * 
 * ArrayList:
 * - Best for frequent retrieval operations
 * - Poor choice for frequent insertion/deletion operations
 * - Uses resizable/growable array as underlying data structure
 * - Implements RandomAccess interface for direct element access
 * - Provides O(1) time complexity for get operations
 * 
 * LinkedList:
 * - Best for frequent insertion and deletion operations
 * - Poor choice for frequent retrieval operations
 * - Uses Double Linked List as underlying data structure
 * - Does not implement RandomAccess interface
 * - Requires traversal for element access, O(n) time complexity for get operations
 * 
 * Key Difference:
 * The RandomAccess interface indicates that ArrayList supports constant-time
 * random access to elements via index, while LinkedList requires sequential
 * traversal from the beginning or end, making retrieval significantly slower.
 
