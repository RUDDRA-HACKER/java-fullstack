
# Collections vs Collection in Java

## Collection (Interface)
- **Single interface** in `java.util` package
- Root interface for all collection types
- Defines common methods: `add()`, `remove()`, `contains()`, `size()`, `iterator()`
- Represents a single group of objects

```java
Collection<String> col = new ArrayList<>();
col.add("item");
```

## Collections (Utility Class)
- **Utility class** with static helper methods
- Provides algorithms and operations for collections
- Methods: `sort()`, `shuffle()`, `reverse()`, `binarySearch()`, `max()`, `min()`
- Cannot be instantiated

```java
Collections.sort(list);
Collections.shuffle(list);
```

## Key Difference

| Feature | Collection | Collections |
|---------|-----------|-------------|
| Type | Interface | Class |
| Purpose | Define collection contract | Provide utility methods |
| Usage | Implement/extend | Call static methods |
| Package | `java.util` | `java.util` |

## Example

```java
List<Integer> nums = new ArrayList<>();
nums.add(5);
nums.add(2);
nums.add(8);

Collections.sort(nums);  // Uses Collections class
System.out.println(nums);  // [2, 5, 8]
```
