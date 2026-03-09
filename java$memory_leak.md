
# Memory Leaks in Java

## What is a Memory Leak?

A memory leak occurs when objects are no longer needed but remain in memory, preventing garbage collection and consuming system resources.

## Common Causes

### 1. **Static Collections**
```java
// BAD: Static list holds references indefinitely
static List<String> cache = new ArrayList<>();
cache.add("data"); // Never removed
```

### 2. **Unclosed Resources**
```java
// BAD: Connection never closed
Connection conn = DriverManager.getConnection(url);
// Missing: conn.close();
```

### 3. **Event Listeners**
```java
// BAD: Listener never unregistered
button.addListener(listener);
// Missing: button.removeListener(listener);
```

### 4. **Circular References**
Objects referencing each other prevent garbage collection.

## Prevention Tips

- **Use try-with-resources** for automatic resource closure
- **Unregister listeners** when objects are destroyed
- **Limit static collections** or use weak references
- **Use WeakHashMap** for caches
- **Monitor with profilers** (JProfiler, YourKit)

## Detection Tools

- JVM Heap Dumps
- Eclipse Memory Analyzer (MAT)
- JVisualVM
- Async Profiler
