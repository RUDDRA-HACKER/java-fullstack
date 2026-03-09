# ☕ Java 8 — Complete Teaching Guide

> **Purpose:** This guide is for teaching students who are new to Java 8.  
> Every concept is explained in plain English first, then shown with code.

---

## 📌 Table of Contents

1. [What is a Lambda?](#1-what-is-a-lambda)
2. [The Syntax — Broken Down](#2-the-syntax--broken-down)
3. [All Lambda Forms — With Examples](#3-all-lambda-forms--with-examples)
4. [Before and After Java 8](#4-before-and-after-java-8)
5. [Functional Interfaces — The Foundation](#5-functional-interfaces--the-foundation)
6. [Built-in Functional Interfaces](#6-built-in-functional-interfaces)
7. [Real-World Use Cases](#7-real-world-use-cases)
8. [Variable Capture Rules](#8-variable-capture-rules)
9. [Method References — Lambda Shorthand](#9-method-references--lambda-shorthand)
10. [Common Mistakes Students Make](#10-common-mistakes-students-make)
11. [Stream API — Full Guide](#11-stream-api--full-guide)
12. [Optional Class — Full Guide](#12-optional-class--full-guide)
13. [New Date/Time API — Full Guide](#13-new-datetime-api--full-guide)
14. [More Lambda Examples — Advanced](#14-more-lambda-examples--advanced)
15. [Quick Reference Card](#15-quick-reference-card)

---

## 1. What is a Lambda?

A **lambda expression** is a short, anonymous function. It has no name, no class, and no access modifier. You write it inline wherever you need a small piece of behavior.

### Simple Analogy

Think of a lambda like a **sticky note instruction**:

- Old way (before Java 8): You write a whole formal document (anonymous inner class) just to say "multiply by 2."
- Lambda way: You just write a sticky note — `x -> x * 2`

The arrow `->` means **"goes to"** or **"do this"**.

---

## 2. The Syntax — Broken Down

```
(parameters)  ->  expression
    |          |       |
  input      arrow   what to do
```

### Three Parts of a Lambda

| Part | Description | Example |
|------|-------------|---------|
| Parameters | The inputs the lambda receives | `(x, y)` or `name` |
| Arrow | Separates input from body | `->` |
| Body | What the lambda does | `x + y` or `{ return x + y; }` |

---

## 3. All Lambda Forms — With Examples

### Form 1 — No Parameters

```java
// When nothing is passed in
() -> System.out.println("Hello!")
() -> "Hello Java 8"
() -> 42
```

### Form 2 — One Parameter (no brackets needed)

```java
// Single parameter — brackets are optional
name -> "Hello, " + name
x -> x * 2
s -> s.toUpperCase()
```

### Form 3 — Multiple Parameters (brackets required)

```java
// Two or more parameters — must use brackets
(a, b) -> a + b
(x, y) -> x * y
(first, last) -> first + " " + last
```

### Form 4 — Block Body (multiple lines)

```java
// Use { } when you have more than one line
(a, b) -> {
    int sum = a + b;
    System.out.println("Sum is: " + sum);
    return sum;
}
```

### Form 5 — With Explicit Types

```java
// You can declare types (but usually Java figures them out)
(int x, int y) -> x + y
(String name, int age) -> name + " is " + age
```

### Form 6 — Void Return (no return value)

```java
// No return — just does something and finishes
name -> System.out.println(name)
x -> list.add(x)
```

---

## 4. Before and After Java 8

### Sorting a List — Old Way

```java
// Java 7 and before — anonymous inner class
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");

Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});
```

### Sorting a List — Lambda Way (Java 8)

```java
// Same result — much shorter!
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");

names.sort((a, b) -> a.compareTo(b));

// Even shorter using method reference:
names.sort(String::compareTo);
```

### Running a Thread — Old Way

```java
Thread t = new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Running in a thread");
    }
});
t.start();
```

### Running a Thread — Lambda Way

```java
Thread t = new Thread(() -> System.out.println("Running in a thread"));
t.start();
```

---

## 5. Functional Interfaces — The Foundation

A lambda expression can only be used where a **Functional Interface** is expected.

### What is a Functional Interface?

An interface with **exactly one abstract method**. That single method is what the lambda provides the body for.

```java
@FunctionalInterface  // This annotation is optional but recommended
interface MathOperation {
    int operate(int a, int b);  // Only ONE abstract method
}
```

### Using it with a Lambda

```java
MathOperation add      = (a, b) -> a + b;
MathOperation multiply = (a, b) -> a * b;
MathOperation subtract = (a, b) -> a - b;

System.out.println(add.operate(5, 3));       // 8
System.out.println(multiply.operate(5, 3));  // 15
System.out.println(subtract.operate(5, 3));  // 2
```

### Teaching Point

> The lambda fills in the "blank" of the one abstract method. Think of the interface as a template with one blank, and the lambda as what you write in that blank.

---

## 6. Built-in Functional Interfaces

Java 8 ships with many ready-made functional interfaces in `java.util.function`:

### Predicate\<T\> — Tests a condition, returns boolean

```java
Predicate<Integer> isEven = n -> n % 2 == 0;
Predicate<String> isEmpty = s -> s.isEmpty();

isEven.test(4);     // true
isEven.test(7);     // false
isEmpty.test("");   // true

// Combining predicates
Predicate<Integer> isPositive = n -> n > 0;
Predicate<Integer> isPositiveEven = isEven.and(isPositive);
isPositiveEven.test(4);   // true
isPositiveEven.test(-4);  // false (negative)
isPositiveEven.test(3);   // false (odd)
```

### Function\<T, R\> — Transforms a value, returns a result

```java
Function<String, Integer> strLength = s -> s.length();
Function<Integer, String> intToStr  = n -> "Number: " + n;
Function<String, String>  shout     = s -> s.toUpperCase() + "!";

strLength.apply("Hello");  // 5
intToStr.apply(42);        // "Number: 42"
shout.apply("java");       // "JAVA!"

// Chaining with andThen
Function<String, String> shoutLength = shout.andThen(s -> s + " (" + s.length() + " chars)");
shoutLength.apply("hi");   // "HI! (3 chars)"
```

### Consumer\<T\> — Takes a value, returns nothing

```java
Consumer<String> printer  = s -> System.out.println(s);
Consumer<String> logger   = s -> System.out.println("[LOG] " + s);

printer.accept("Hello");   // prints: Hello
logger.accept("Error");    // prints: [LOG] Error

// Chaining consumers
Consumer<String> both = printer.andThen(logger);
both.accept("Test");       // prints: Test, then [LOG] Test
```

### Supplier\<T\> — Takes nothing, provides a value

```java
Supplier<String>  greeting = () -> "Hello World";
Supplier<Integer> randomNum = () -> (int)(Math.random() * 100);
Supplier<List<String>> newList = () -> new ArrayList<>();

greeting.get();    // "Hello World"
randomNum.get();   // some random number
newList.get();     // a new empty ArrayList
```

### BiFunction\<T, U, R\> — Takes two inputs, returns one result

```java
BiFunction<String, Integer, String> repeat = (s, n) -> s.repeat(n);
BiFunction<Integer, Integer, Integer> power = (base, exp) -> (int) Math.pow(base, exp);

repeat.apply("Hi ", 3);   // "Hi Hi Hi "
power.apply(2, 10);       // 1024
```

### UnaryOperator\<T\> — Input and output are the same type

```java
UnaryOperator<String>  addExclaim = s -> s + "!";
UnaryOperator<Integer> doubleIt   = n -> n * 2;
UnaryOperator<String>  trim       = String::trim;

addExclaim.apply("Java");   // "Java!"
doubleIt.apply(5);          // 10
```

### BinaryOperator\<T\> — Two inputs of same type, one output of same type

```java
BinaryOperator<Integer> add    = (a, b) -> a + b;
BinaryOperator<String>  concat = (a, b) -> a + b;

add.apply(3, 5);         // 8
concat.apply("Hi ", "there");  // "Hi there"
```

---

## 7. Real-World Use Cases

### Use Case 1 — Filter a List of Students

```java
List<String> students = Arrays.asList("Alice", "Bob", "Anna", "Charlie", "Amy");

// Get all students whose name starts with "A"
List<String> aStudents = students.stream()
    .filter(name -> name.startsWith("A"))
    .collect(Collectors.toList());

System.out.println(aStudents);  // [Alice, Anna, Amy]
```

### Use Case 2 — Transform a List (map)

```java
List<String> names = Arrays.asList("alice", "bob", "charlie");

// Convert all names to uppercase
List<String> upper = names.stream()
    .map(name -> name.toUpperCase())
    .collect(Collectors.toList());

// [ALICE, BOB, CHARLIE]
```

### Use Case 3 — Sort Students by Name Length

```java
List<String> names = Arrays.asList("Charlie", "Al", "Bob", "Alexander");

names.sort((a, b) -> Integer.compare(a.length(), b.length()));
// [Al, Bob, Charlie, Alexander]
```

### Use Case 4 — forEach on a Map

```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 95);
scores.put("Bob", 82);
scores.put("Charlie", 90);

scores.forEach((name, score) ->
    System.out.println(name + " scored " + score));
```

### Use Case 5 — Find the Highest Score

```java
List<Integer> scores = Arrays.asList(85, 92, 78, 96, 88);

Optional<Integer> highest = scores.stream()
    .max((a, b) -> a.compareTo(b));

highest.ifPresent(h -> System.out.println("Highest: " + h));  // 96
```

### Use Case 6 — Button Click in Swing (GUI)

```java
JButton button = new JButton("Click Me");

// Old way:
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button clicked!");
    }
});

// Lambda way:
button.addActionListener(e -> System.out.println("Button clicked!"));
```

---

## 8. Variable Capture Rules

Lambdas can access variables from outside their own scope — this is called **variable capture**.

### Rule: Variables must be "effectively final"

A variable is effectively final if its value is never changed after the lambda uses it.

```java
// ✅ CORRECT — prefix is never changed
String prefix = "Hello";
Consumer<String> greeter = name -> System.out.println(prefix + " " + name);
greeter.accept("Alice");  // Hello Alice

// ❌ COMPILE ERROR — prefix is changed after capture
String greeting = "Hi";
greeting = "Hello";  // This makes it NOT effectively final
Consumer<String> g = name -> System.out.println(greeting + name);  // ERROR!
```

### What Lambdas Can Access

| Variable Type | Can Access? | Notes |
|---------------|-------------|-------|
| Local variables | ✅ Yes | Must be effectively final |
| Instance fields | ✅ Yes | Can read and modify |
| Static fields | ✅ Yes | Can read and modify |
| Method parameters | ✅ Yes | Must be effectively final |

---

## 9. Method References — Lambda Shorthand

When a lambda just calls one existing method and passes its argument, you can shorten it to a **method reference** using `::`.

### The Four Types

| Type | Lambda | Method Reference |
|------|--------|-----------------|
| Static method | `x -> Integer.parseInt(x)` | `Integer::parseInt` |
| Instance method (specific object) | `x -> obj.equals(x)` | `obj::equals` |
| Instance method (any object of type) | `x -> x.toLowerCase()` | `String::toLowerCase` |
| Constructor | `() -> new ArrayList<>()` | `ArrayList::new` |

### Examples

```java
// 1. Static method reference
List<String> nums = Arrays.asList("3", "1", "2");
nums.stream()
    .map(Integer::parseInt)   // same as: x -> Integer.parseInt(x)
    .forEach(System.out::println);

// 2. Instance method of specific object
String target = "Java";
Predicate<String> isJava = target::equals;  // same as: s -> target.equals(s)
isJava.test("Java");   // true
isJava.test("Python"); // false

// 3. Instance method of any object (arbitrary instance)
List<String> words = Arrays.asList("hello", "world");
words.stream()
    .map(String::toUpperCase)  // same as: s -> s.toUpperCase()
    .forEach(System.out::println);

// 4. Constructor reference
Supplier<ArrayList<String>> listMaker = ArrayList::new;  // same as: () -> new ArrayList<>()
ArrayList<String> myList = listMaker.get();
```

---

## 10. Common Mistakes Students Make

### Mistake 1 — Forgetting the target type

```java
// ❌ ERROR — Java doesn't know what type this lambda is
var fn = x -> x * 2;  // ERROR: what interface is this?

// ✅ CORRECT — provide the target type
Function<Integer, Integer> fn = x -> x * 2;
```

### Mistake 2 — Returning in a single-expression lambda

```java
// ❌ WRONG — don't use 'return' in expression lambdas
Function<Integer, Integer> fn = x -> return x * 2;  // Compile error!

// ✅ CORRECT for expression lambda
Function<Integer, Integer> fn1 = x -> x * 2;

// ✅ CORRECT for block lambda (use return inside {})
Function<Integer, Integer> fn2 = x -> { return x * 2; };
```

### Mistake 3 — Modifying a local variable inside a lambda

```java
int count = 0;
list.forEach(item -> {
    count++;  // ❌ ERROR: count is captured, cannot be modified
});

// ✅ Use an array or AtomicInteger as a workaround
int[] count = {0};
list.forEach(item -> count[0]++);  // Works!

// Or better:
long count = list.stream().count();  // Cleanest way
```

### Mistake 4 — Expecting a lambda to run immediately

```java
Runnable r = () -> System.out.println("Hello");
// Nothing printed yet! The lambda is just defined, not run.

r.run();  // NOW it runs and prints "Hello"
```

---

---

## 11. Stream API — Full Guide

### What is a Stream?

A **Stream** is a sequence of elements that you can process step by step. It is NOT a data structure — it does not store data. It reads from a source (like a List or Array) and processes it through a pipeline of steps.

> Think of a Stream like a factory conveyor belt. Raw materials (your data) go in one end, pass through several machines (operations), and finished products (results) come out the other end.

### The Three Parts of a Stream Pipeline

```
Source  →  Intermediate Operations  →  Terminal Operation
  |                  |                        |
 List            filter, map, sort        collect, count, forEach
```

### Creating a Stream

```java
// From a List
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Stream<String> stream1 = names.stream();

// From an Array
String[] arr = {"Alice", "Bob"};
Stream<String> stream2 = Arrays.stream(arr);

// From values directly
Stream<String> stream3 = Stream.of("Alice", "Bob", "Charlie");

// Empty stream
Stream<String> empty = Stream.empty();

// Infinite stream (use limit to stop it!)
Stream<Integer> infinite = Stream.iterate(0, n -> n + 1);
```

---

### Intermediate Operations — These Transform the Stream

Intermediate operations are **lazy** — they don't run until a terminal operation is called.

#### filter() — Keep only matching elements

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)       // keep only even numbers
    .collect(Collectors.toList());

// [2, 4, 6, 8, 10]
```

#### map() — Transform each element

```java
List<String> names = Arrays.asList("alice", "bob", "charlie");

List<String> upper = names.stream()
    .map(name -> name.toUpperCase())   // transform each name
    .collect(Collectors.toList());

// [ALICE, BOB, CHARLIE]

// Map to a different type
List<Integer> lengths = names.stream()
    .map(name -> name.length())        // String → Integer
    .collect(Collectors.toList());

// [5, 3, 7]
```

#### sorted() — Sort elements

```java
List<Integer> nums = Arrays.asList(5, 3, 8, 1, 4);

// Natural order
List<Integer> sorted = nums.stream()
    .sorted()
    .collect(Collectors.toList());
// [1, 3, 4, 5, 8]

// Custom order (descending)
List<Integer> desc = nums.stream()
    .sorted((a, b) -> b - a)
    .collect(Collectors.toList());
// [8, 5, 4, 3, 1]
```

#### distinct() — Remove duplicates

```java
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 3, 3, 4);

List<Integer> unique = nums.stream()
    .distinct()
    .collect(Collectors.toList());
// [1, 2, 3, 4]
```

#### limit() — Take only the first N elements

```java
List<Integer> nums = Arrays.asList(10, 20, 30, 40, 50, 60);

List<Integer> firstThree = nums.stream()
    .limit(3)
    .collect(Collectors.toList());
// [10, 20, 30]
```

#### skip() — Skip the first N elements

```java
List<Integer> nums = Arrays.asList(10, 20, 30, 40, 50);

List<Integer> afterTwo = nums.stream()
    .skip(2)
    .collect(Collectors.toList());
// [30, 40, 50]
```

#### peek() — Look at elements without changing them (great for debugging)

```java
List<Integer> result = nums.stream()
    .filter(n -> n > 2)
    .peek(n -> System.out.println("After filter: " + n))  // debug
    .map(n -> n * 10)
    .peek(n -> System.out.println("After map: " + n))     // debug
    .collect(Collectors.toList());
```

---

### Terminal Operations — These Produce a Result

Terminal operations **trigger** the whole pipeline and produce a final result.

#### forEach() — Do something with each element

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.stream().forEach(name -> System.out.println("Hello, " + name));
```

#### collect() — Gather results into a collection

```java
// To List
List<String> list = stream.collect(Collectors.toList());

// To Set (removes duplicates)
Set<String> set = stream.collect(Collectors.toSet());

// To specific collection
LinkedList<String> linked = stream.collect(Collectors.toCollection(LinkedList::new));

// Join into a String
String joined = names.stream().collect(Collectors.joining(", "));
// "Alice, Bob, Charlie"

String joinedWithBrackets = names.stream()
    .collect(Collectors.joining(", ", "[", "]"));
// "[Alice, Bob, Charlie]"
```

#### count() — Count the elements

```java
long count = names.stream()
    .filter(n -> n.startsWith("A"))
    .count();
// 1
```

#### findFirst() / findAny() — Get one element

```java
Optional<String> first = names.stream()
    .filter(n -> n.length() > 3)
    .findFirst();

first.ifPresent(n -> System.out.println("Found: " + n));  // Found: Alice
```

#### min() / max() — Find smallest or largest

```java
List<Integer> nums = Arrays.asList(5, 3, 8, 1, 4);

Optional<Integer> min = nums.stream().min(Integer::compareTo);  // 1
Optional<Integer> max = nums.stream().max(Integer::compareTo);  // 8
```

#### reduce() — Combine all elements into one value

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);

// Sum all numbers
int sum = nums.stream()
    .reduce(0, (a, b) -> a + b);   // 0 is the starting value
// sum = 15

// Multiply all numbers
int product = nums.stream()
    .reduce(1, (a, b) -> a * b);
// product = 120
```

#### anyMatch / allMatch / noneMatch — Check conditions

```java
List<Integer> nums = Arrays.asList(2, 4, 6, 7, 8);

boolean anyOdd  = nums.stream().anyMatch(n -> n % 2 != 0);   // true  (7 is odd)
boolean allEven = nums.stream().allMatch(n -> n % 2 == 0);   // false (7 is not even)
boolean noneNeg = nums.stream().noneMatch(n -> n < 0);       // true  (none are negative)
```

---

### Chaining Multiple Operations Together

```java
List<String> students = Arrays.asList(
    "Alice", "Bob", "Anna", "Charlie", "Amy", "Ben"
);

// Find all students whose name starts with "A",
// sort them alphabetically,
// convert to uppercase,
// and collect into a list
List<String> result = students.stream()
    .filter(name -> name.startsWith("A"))    // Alice, Anna, Amy
    .sorted()                                // Alice, Amy, Anna
    .map(String::toUpperCase)                // ALICE, AMY, ANNA
    .collect(Collectors.toList());

System.out.println(result);  // [ALICE, AMY, ANNA]
```

### Numeric Streams — IntStream, LongStream, DoubleStream

```java
// Sum numbers 1 to 10
int sum = IntStream.rangeClosed(1, 10).sum();  // 55

// Average of a list
OptionalDouble avg = IntStream.of(10, 20, 30, 40).average();
avg.ifPresent(a -> System.out.println("Average: " + a));  // 25.0

// Convert List<Integer> to IntStream
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
int total = nums.stream()
    .mapToInt(Integer::intValue)
    .sum();  // 15
```

> **Teaching Tip:** Draw the pipeline on the board as boxes connected by arrows. Show data flowing through each box and transforming. This visual makes streams click for students immediately.

---

## 12. Optional Class — Full Guide

### The Problem Optional Solves

Before Java 8, methods that might not have a value to return would return `null`. This caused crashes called **NullPointerException (NPE)** — one of the most common Java bugs.

```java
// Old way — dangerous!
String name = findStudent("id123");  // might return null
System.out.println(name.toUpperCase());  // CRASH if name is null!

// You had to write null checks everywhere
if (name != null) {
    System.out.println(name.toUpperCase());
}
```

Optional forces you to **acknowledge that a value might be absent** and handle it properly.

---

### Creating Optional Objects

```java
// Optional.of() — use when you KNOW the value is not null
Optional<String> name = Optional.of("Alice");

// Optional.empty() — represents "no value"
Optional<String> empty = Optional.empty();

// Optional.ofNullable() — use when value MIGHT be null
String value = null;
Optional<String> maybe = Optional.ofNullable(value);  // empty Optional
```

> ⚠️ Never use `Optional.of(null)` — it will throw a NullPointerException immediately.

---

### Checking and Getting the Value

```java
Optional<String> opt = Optional.of("Hello Java 8");

// isPresent() — check if value exists
if (opt.isPresent()) {
    System.out.println(opt.get());  // Hello Java 8
}

// isEmpty() — Java 11+ check if empty (opposite of isPresent)
if (opt.isEmpty()) {
    System.out.println("No value here");
}
```

---

### Safe Ways to Retrieve the Value

```java
Optional<String> name = Optional.of("Alice");
Optional<String> empty = Optional.empty();

// orElse() — return a default value if empty
String result1 = name.orElse("Unknown");    // "Alice"
String result2 = empty.orElse("Unknown");   // "Unknown"

// orElseGet() — compute the default only if needed (lazy)
String result3 = empty.orElseGet(() -> "Default from supplier");

// orElseThrow() — throw an exception if empty
String result4 = name.orElseThrow(() -> new RuntimeException("Not found!"));

// ifPresent() — run lambda only if value exists
name.ifPresent(n -> System.out.println("Hello, " + n));   // Hello, Alice
empty.ifPresent(n -> System.out.println("Hello, " + n));  // (nothing happens)
```

---

### Transforming Optional Values

```java
Optional<String> name = Optional.of("alice");

// map() — transform the value inside Optional
Optional<String> upper = name.map(String::toUpperCase);
upper.ifPresent(System.out::println);  // ALICE

// map() returns empty Optional if original was empty
Optional<String> empty = Optional.empty();
Optional<String> result = empty.map(String::toUpperCase);
// result is also empty — no crash!

// filter() — keep value only if it passes the condition
Optional<String> longName = name.filter(n -> n.length() > 3);
// present, because "alice" has 5 characters

Optional<String> shortName = name.filter(n -> n.length() > 10);
// empty, because "alice" is not longer than 10
```

---

### Real-World Optional Example

```java
// Simulating a student lookup
public Optional<String> findStudentById(int id) {
    Map<Integer, String> db = Map.of(1, "Alice", 2, "Bob");
    return Optional.ofNullable(db.get(id));
}

// Using it safely
Optional<String> student = findStudentById(1);
String name = student
    .map(String::toUpperCase)
    .orElse("Student not found");

System.out.println(name);  // ALICE

Optional<String> missing = findStudentById(99);
String name2 = missing
    .map(String::toUpperCase)
    .orElse("Student not found");

System.out.println(name2);  // Student not found
```

### Optional — Do's and Don'ts

| ✅ Do | ❌ Don't |
|-------|---------|
| Use Optional as a return type | Use Optional as a field in a class |
| Use orElse / ifPresent | Call .get() without checking isPresent() |
| Use map/filter on Optional | Pass Optional as a method parameter |
| Return Optional.empty() instead of null | Use Optional.of() with a potentially null value |

> **Teaching Tip:** Ask students to imagine Optional as a "maybe box." The box might have something inside or might be empty. You should always check before reaching in!

---

## 13. New Date/Time API — Full Guide

### Why Java 8 Introduced a New API

The old `java.util.Date` and `java.util.Calendar` classes had serious problems:

- They were **mutable** — the date could be accidentally changed
- They were **not thread-safe** — problems in multi-threaded programs
- The API was confusing — months started at 0 (January = 0!)
- No clear separation between date, time, and date-time

Java 8 introduced `java.time` package — immutable, clear, and easy to use.

---

### The Main Classes

| Class | What it Represents | Example |
|-------|--------------------|---------|
| `LocalDate` | Date only (no time, no timezone) | 2024-03-09 |
| `LocalTime` | Time only (no date) | 10:30:45 |
| `LocalDateTime` | Date and time (no timezone) | 2024-03-09T10:30:45 |
| `ZonedDateTime` | Date, time, and timezone | 2024-03-09T10:30:45+05:30 |
| `Instant` | A moment on the timeline (UTC) | Unix timestamp |
| `Period` | Amount of time in years/months/days | 2 years, 3 months |
| `Duration` | Amount of time in hours/minutes/seconds | 5 hours, 30 minutes |
| `DateTimeFormatter` | Formats and parses dates | "dd/MM/yyyy" |

---

### LocalDate — Working with Dates

```java
import java.time.LocalDate;

// Create dates
LocalDate today     = LocalDate.now();              // current date
LocalDate birthday  = LocalDate.of(2000, 5, 15);   // May 15, 2000
LocalDate fromText  = LocalDate.parse("2024-03-09"); // from a String

System.out.println(today);     // 2024-03-09  (your current date)
System.out.println(birthday);  // 2000-05-15

// Get parts of a date
int year  = today.getYear();          // 2024
int month = today.getMonthValue();    // 3 (March — starts at 1, not 0!)
int day   = today.getDayOfMonth();    // 9
String dayName = today.getDayOfWeek().toString();  // SATURDAY

// Add or subtract
LocalDate nextWeek    = today.plusDays(7);
LocalDate lastMonth   = today.minusMonths(1);
LocalDate nextYear    = today.plusYears(1);

// Compare dates
boolean isBefore  = birthday.isBefore(today);   // true
boolean isAfter   = today.isAfter(birthday);     // true
boolean isEqual   = today.isEqual(today);        // true

// Check if leap year
boolean isLeap = LocalDate.of(2024, 1, 1).isLeapYear();  // true
```

---

### LocalTime — Working with Times

```java
import java.time.LocalTime;

// Create times
LocalTime now       = LocalTime.now();           // current time
LocalTime lunch     = LocalTime.of(12, 30);      // 12:30:00
LocalTime precise   = LocalTime.of(10, 15, 45);  // 10:15:45

// Get parts
int hour   = lunch.getHour();    // 12
int minute = lunch.getMinute();  // 30
int second = lunch.getSecond();  // 0

// Add or subtract
LocalTime later    = lunch.plusHours(2);     // 14:30
LocalTime earlier  = lunch.minusMinutes(30); // 12:00

// Compare
boolean isBefore = LocalTime.of(9, 0).isBefore(lunch);  // true
```

---

### LocalDateTime — Date and Time Together

```java
import java.time.LocalDateTime;

// Create
LocalDateTime now = LocalDateTime.now();
LocalDateTime meeting = LocalDateTime.of(2024, 3, 15, 10, 30, 0);

// Combine a LocalDate and LocalTime
LocalDate date = LocalDate.of(2024, 3, 15);
LocalTime time = LocalTime.of(10, 30);
LocalDateTime combined = LocalDateTime.of(date, time);

// Extract parts
LocalDate datePart = meeting.toLocalDate();
LocalTime timePart = meeting.toLocalTime();

System.out.println(meeting);  // 2024-03-15T10:30
```

---

### Period — Measuring Gaps Between Dates

```java
import java.time.Period;

LocalDate birthDate = LocalDate.of(2000, 5, 15);
LocalDate today     = LocalDate.now();

Period age = Period.between(birthDate, today);

System.out.println("Age: " + age.getYears() + " years, "
                            + age.getMonths() + " months, "
                            + age.getDays() + " days");

// Create a period directly
Period twoYears = Period.ofYears(2);
Period sixMonths = Period.ofMonths(6);

// Add period to a date
LocalDate future = today.plus(Period.of(1, 6, 0));  // 1 year, 6 months from now
```

---

### Duration — Measuring Time Gaps

```java
import java.time.Duration;
import java.time.LocalTime;

LocalTime start = LocalTime.of(9, 0);
LocalTime end   = LocalTime.of(17, 30);

Duration workDay = Duration.between(start, end);

System.out.println("Hours: " + workDay.toHours());    // 8
System.out.println("Minutes: " + workDay.toMinutes()); // 510

// Create duration directly
Duration twoHours = Duration.ofHours(2);
Duration thirtyMins = Duration.ofMinutes(30);
```

---

### DateTimeFormatter — Formatting and Parsing

```java
import java.time.format.DateTimeFormatter;

LocalDate date = LocalDate.of(2024, 3, 9);

// Format a date into a String
DateTimeFormatter formatter1 = DateTimeFormatter.ofPattern("dd/MM/yyyy");
DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("MMMM dd, yyyy");
DateTimeFormatter formatter3 = DateTimeFormatter.ofPattern("dd-MMM-yyyy");

System.out.println(date.format(formatter1));  // 09/03/2024
System.out.println(date.format(formatter2));  // March 09, 2024
System.out.println(date.format(formatter3));  // 09-Mar-2024

// Parse a String into a LocalDate
LocalDate parsed = LocalDate.parse("09/03/2024", formatter1);
System.out.println(parsed);  // 2024-03-09
```

---

### Before vs After — The Improvement

```java
// OLD WAY — confusing and error-prone
Calendar cal = Calendar.getInstance();
cal.set(2000, 4, 15);  // Month is 4 — but that means MAY (starts from 0!)
Date oldDate = cal.getTime();

// NEW WAY — clean and readable
LocalDate newDate = LocalDate.of(2000, 5, 15);  // Month 5 = May. Simple!
```

> **Teaching Tip:** Tell students: "In the old API, January = 0, December = 11. How many bugs do you think that caused? The new API fixed this — January = 1."

---

## 14. More Lambda Examples — Advanced

### Example 1 — Chaining Predicates

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Predicate<Integer> isEven    = n -> n % 2 == 0;
Predicate<Integer> isGreater = n -> n > 5;

// and() — both must be true
List<Integer> evenAndBig = numbers.stream()
    .filter(isEven.and(isGreater))
    .collect(Collectors.toList());
// [6, 8, 10]

// or() — either must be true
List<Integer> evenOrBig = numbers.stream()
    .filter(isEven.or(isGreater))
    .collect(Collectors.toList());
// [2, 4, 6, 7, 8, 9, 10]

// negate() — flip the result
List<Integer> notEven = numbers.stream()
    .filter(isEven.negate())
    .collect(Collectors.toList());
// [1, 3, 5, 7, 9]
```

---

### Example 2 — Chaining Functions

```java
Function<String, String> trim     = String::trim;
Function<String, String> upper    = String::toUpperCase;
Function<String, String> addHello = s -> "Hello, " + s;

// andThen — apply functions in sequence
Function<String, String> pipeline = trim.andThen(upper).andThen(addHello);

System.out.println(pipeline.apply("  alice  "));  // Hello, ALICE

// compose — apply in reverse order (inner first)
Function<String, String> composed = addHello.compose(upper.compose(trim));
System.out.println(composed.apply("  alice  "));  // Hello, ALICE
```

---

### Example 3 — Lambda with Custom Object

```java
class Student {
    String name;
    int grade;
    Student(String name, int grade) {
        this.name = name;
        this.grade = grade;
    }
    public String getName()  { return name; }
    public int    getGrade() { return grade; }
}

List<Student> students = Arrays.asList(
    new Student("Alice", 92),
    new Student("Bob", 75),
    new Student("Charlie", 88),
    new Student("Anna", 95)
);

// Sort by grade descending
students.sort((a, b) -> b.getGrade() - a.getGrade());

// Get names of students who passed (grade >= 80)
List<String> passed = students.stream()
    .filter(s -> s.getGrade() >= 80)
    .map(Student::getName)
    .sorted()
    .collect(Collectors.toList());

System.out.println(passed);  // [Alice, Anna, Charlie]

// Find top student
Optional<Student> top = students.stream()
    .max((a, b) -> Integer.compare(a.getGrade(), b.getGrade()));

top.ifPresent(s -> System.out.println("Top: " + s.getName() + " (" + s.getGrade() + ")"));
// Top: Anna (95)

// Calculate average grade
double avg = students.stream()
    .mapToInt(Student::getGrade)
    .average()
    .orElse(0);

System.out.println("Average: " + avg);  // Average: 87.5
```

---

### Example 4 — Grouping with Collectors

```java
List<String> words = Arrays.asList(
    "apple", "banana", "avocado", "blueberry", "cherry", "apricot"
);

// Group by first letter
Map<Character, List<String>> grouped = words.stream()
    .collect(Collectors.groupingBy(w -> w.charAt(0)));

grouped.forEach((letter, list) ->
    System.out.println(letter + ": " + list));
// a: [apple, avocado, apricot]
// b: [banana, blueberry]
// c: [cherry]

// Count words per first letter
Map<Character, Long> counts = words.stream()
    .collect(Collectors.groupingBy(w -> w.charAt(0), Collectors.counting()));
// {a=3, b=2, c=1}
```

---

### Example 5 — FlatMap (Flattening Nested Lists)

```java
List<List<Integer>> nested = Arrays.asList(
    Arrays.asList(1, 2, 3),
    Arrays.asList(4, 5),
    Arrays.asList(6, 7, 8, 9)
);

// flatMap flattens the nested lists into one stream
List<Integer> flat = nested.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());

System.out.println(flat);  // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Real example — get all unique words from multiple sentences
List<String> sentences = Arrays.asList(
    "Java is great",
    "Lambda is powerful",
    "Java 8 is modern"
);

List<String> uniqueWords = sentences.stream()
    .flatMap(sentence -> Arrays.stream(sentence.split(" ")))
    .distinct()
    .sorted()
    .collect(Collectors.toList());

System.out.println(uniqueWords);
// [10, Lambda, Java, great, is, modern, powerful]
```

---

### Example 6 — Lazy Evaluation in Action

```java
// Streams are lazy — operations only run when needed
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// This stops as soon as it finds the first match
Optional<Integer> firstEvenOver5 = numbers.stream()
    .filter(n -> {
        System.out.println("Checking filter: " + n);
        return n % 2 == 0;
    })
    .filter(n -> n > 5)
    .findFirst();

// It won't process all 10 numbers — it stops at 6!
System.out.println("Found: " + firstEvenOver5.get());  // 6
```

---

## 15. Quick Reference Card

```
LAMBDA SYNTAX
─────────────────────────────────────────────────────
()             -> expression         No parameters
x              -> expression         One parameter
(x, y)         -> expression         Two parameters
(x, y)         -> { statements; }   Block body
(int x, int y) -> x + y             Explicit types

COMMON FUNCTIONAL INTERFACES
─────────────────────────────────────────────────────
Predicate<T>         T → boolean        .test()
Function<T,R>        T → R              .apply()
Consumer<T>          T → void           .accept()
Supplier<T>          () → T             .get()
BiFunction<T,U,R>    T,U → R            .apply()
UnaryOperator<T>     T → T              .apply()
BinaryOperator<T>    T,T → T            .apply()
Runnable             () → void          .run()
Callable<V>          () → V             .call()

METHOD REFERENCE TYPES
─────────────────────────────────────────────────────
Static          ClassName::methodName
Instance (obj)  objectRef::methodName
Instance (any)  ClassName::methodName
Constructor     ClassName::new

STREAM OPERATIONS
─────────────────────────────────────────────────────
INTERMEDIATE (lazy)     TERMINAL (triggers pipeline)
filter(predicate)       forEach(consumer)
map(function)           collect(collector)
sorted(comparator)      count()
distinct()              min() / max()
limit(n)                reduce(identity, accumulator)
skip(n)                 findFirst() / findAny()
peek(consumer)          anyMatch / allMatch / noneMatch
flatMap(function)       toArray()

OPTIONAL METHODS
─────────────────────────────────────────────────────
Optional.of(value)         Create with non-null value
Optional.empty()           Create empty Optional
Optional.ofNullable(val)   Create, allows null
.isPresent()               Check if value exists
.get()                     Get value (risky — check first)
.orElse(default)           Get value or default
.orElseGet(supplier)       Get value or compute default
.orElseThrow(exception)    Get value or throw
.ifPresent(consumer)       Run code if value exists
.map(function)             Transform value inside
.filter(predicate)         Keep value if condition passes

DATE/TIME CLASSES
─────────────────────────────────────────────────────
LocalDate          Date only           .now() / .of(y,m,d)
LocalTime          Time only           .now() / .of(h,m,s)
LocalDateTime      Date + Time         .now() / .of(date,time)
ZonedDateTime      Date + Time + Zone  .now(ZoneId)
Period             Date gap            .between(d1, d2)
Duration           Time gap            .between(t1, t2)
DateTimeFormatter  Format/Parse        .ofPattern("dd/MM/yyyy")
```

---

*Complete guide prepared for Java 8 teaching. All examples are self-contained and beginner-friendly.*