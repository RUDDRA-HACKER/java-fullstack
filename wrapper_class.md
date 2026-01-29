## What is a Wrapper Class (Java)

### In Java, a wrapper class is a class that converts a primitive data type into an object.

### Java has primitive types like:

int

double

char

boolean

### But sometimes Java needs objects, not primitives (for example: collections, generics).

That’s where wrapper classes come in.

Primitive → Wrapper class

int → Integer

double → Double

char → Character

boolean → Boolean

## Why Wrapper Classes Are Needed
### Wrapper classes are required in Java for the following reasons:

### Java collections (ArrayList, HashMap, etc.) store only objects, not primitives.
### Wrapper objects allow primitives to be used in object-oriented features like methods, synchronization, and serialization.
### Objects support null values, while primitives do not.
### Wrapper classes provide utility methods such as compareTo(), equals(), and toString().

