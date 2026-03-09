
# How Java Stores Objects in Memory

## Object Storage Mechanism

### Stack vs Heap
- **Stack**: Stores primitive values and object references (memory addresses)
- **Heap**: Stores actual object data
- When you create an object, the reference goes on the stack, and the object lives on the heap

```java
Person person = new Person("John"); // Reference on stack, object on heap
int age = 25; // Primitive value directly on stack
```

## Why Java Object Storage is Efficient

### 1. **Automatic Memory Management (Garbage Collection)**
- Automatically frees unused objects
- No manual memory deallocation needed
- Reduces memory leaks

### 2. **Reference-Based Access**
- Objects accessed via memory addresses, not copied
- Passing objects to methods passes references (lightweight)
- Avoids expensive data duplication

```java
void modifyObject(Person p) {
    p.setName("Jane"); // Modifies original object
}
```

### 3. **Heap Memory Optimization**
- Contiguous memory allocation
- Fast object creation
- Efficient garbage collection algorithms

### 4. **JIT Compilation**
- Just-In-Time compiler optimizes frequently used code
- Converts bytecode to native machine code
- Significantly improves runtime performance

## Memory Layout Example

```
STACK                  HEAP
┌─────────────────┐    ┌──────────────┐
│ person ────────┼───→ │ Person Object│
│ age: 25         │    │ name: "John" │
└─────────────────┘    │ age: 30      │
                       └──────────────┘
```
