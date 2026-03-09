# Stack vs Heap in Java

## Stack
- **Structure**: Linear, LIFO (Last In First Out)
- **Memory**: Fixed size, allocated at compile time
- **Speed**: Faster access
- **Storage**: Primitive values and object references
- **Scope**: Limited to method/block scope
- **Cleanup**: Automatic when scope ends

## Heap
- **Structure**: Hierarchical, dynamic
- **Memory**: Dynamic size, allocated at runtime
- **Speed**: Slower access
- **Storage**: Actual objects and arrays
- **Scope**: Global, persists until garbage collected
- **Cleanup**: Garbage collector manages cleanup

## Key Differences
| Feature | Stack | Heap |
|---------|-------|------|
| Size | Limited, fixed | Large, dynamic |
| Speed | Faster | Slower |
| Thread-safe | Yes (per thread) | No (shared) |
| Overflow | StackOverflowError | OutOfMemoryError |

## Example
```java
int age = 25;           // Stack: primitive value
String name = "John";   // Stack: reference, Heap: actual String object
```
## When to Use Stack vs Heap

**Use Stack when:**
- Working with primitive data types
- Need fast, predictable memory management
- Variables have short, well-defined lifespans

**Use Heap when:**
- Creating objects and complex data structures
- Need dynamic memory allocation
- Objects must persist beyond method scope

## Memory Management Tips

- Stack memory is automatically freed when variables go out of scope
- Heap objects remain until garbage collection occurs
- Large objects should be allocated on the Heap
- Stack overflow occurs with deep recursion or large local arrays
- OutOfMemoryError happens when Heap is exhausted

## Performance Considerations

- Stack allocation is O(1) and very efficient
- Heap allocation involves the memory allocator and is slower
- Garbage collection pauses can impact performance
- Consider object pooling for frequently allocated objects