
# Java Garbage Collection

## Overview
Garbage Collection (GC) is an automatic memory management mechanism that frees up memory by removing objects that are no longer in use.

## How It Works
- JVM automatically identifies unused objects
- Reclaims memory occupied by unreachable objects
- Prevents memory leaks in most cases

## Garbage Collectors in Java

### 1. Serial GC
- Single-threaded collector
- Suitable for small applications
- Flag: `-XX:+UseSerialGC`

### 2. Parallel GC
- Multi-threaded collection
- Better for throughput on multi-core systems
- Flag: `-XX:+UseParallelGC`

### 3. CMS (Concurrent Mark Sweep)
- Low latency garbage collector
- Runs concurrently with application
- Deprecated in newer Java versions

### 4. G1GC (Garbage First)
- Divides heap into regions
- Predictable pause times
- Default in Java 9+
- Flag: `-XX:+UseG1GC`

### 5. ZGC & Shenandoah
- Ultra-low latency
- Sub-millisecond pause times
- For high-performance applications

## Generational Hypothesis
- Young Generation: Short-lived objects
- Old Generation: Long-lived objects
- Most objects die young

## GC Monitoring
```bash
jstat -gc <pid> <interval>
jmap -heap <pid>
```

## Best Practices
- Minimize object creation in loops
- Use object pooling where applicable
- Monitor GC overhead
- Avoid holding references to objects you no longer need
- Use weak references for cache objects
- Profile your application to identify GC bottlenecks
- Keep heap size appropriate for your workload