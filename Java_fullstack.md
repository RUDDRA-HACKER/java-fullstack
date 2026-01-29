# java-fullstack
## **(core java )**
## Basic
### Introduction
### Download and Install Java
### JDK vs JRE vs JVM
### [Identifiers](java$identifier.md)
### [Keywords](java$keyword.md)
### Quiz: Java Basics
### [Data Types](java$datatypes.md)
### [Wrapper Classes](wrapper_class.md)
### [Variables](java$variable.md)
### [Operators](java$operator.md)
### Quiz: Variables, Operator
### [   Decision Making](java$decision_making.md)
### [Loops & Jump Statements](java$loops_and_jump_statement.md)
### Quiz: Control Statements and Loops
### Project: Number Guessing Game


### [Methods in Java](java$method_in_java.md)

### Array
### Quiz: Array
### Projects: Tic-Tac-Toe Game

### [Strings in Java](java$strings.md)
### Quiz: String Classes

## OOP Concepts

### Introduction
### Classes and Objects
### Quiz: Classes and Objects
### Constructors
### Quiz: Constructors
### Object Class
### Abstraction
### Encapsulation
### Inheritance
### Quiz: Inheritance and Abstraction
### Polymorphism
### Packages
### Quiz: Polymorphism and Packages
### Project: Simple Banking Application


## Interfaces
### Interfaces
### Class vs Interface
### Quiz: Interfaces
### Functional Interface
### Nested Interface
### Marker Interface
### Quiz: Interface types and Comparator
### Project: Employee Management System

## Exception Handling

### Exceptions
### Quiz: Java Exceptions
### Final, Finally and Finalize
### Throw and Throws
### Customized Exception Handling
### Chained Exceptions
### Null Pointer Exceptions
### Exception Handling with Method Overriding
### Quiz: Exception Handling

## Regex

### Introduction
### Matcher Class
### Character Class
### Quantifiers
### Quiz: Regex Basics and Pattern Matching


## Memory Allocation

### Java Memory Management
### How Java Objects Stored in Memory?
### Quiz: Java Memory Allocation
### Types of Memory Areas Allocated by JVM
### Stack vs Heap Memory Allocation
### Quiz: Heap vs Stack
### Garbage Collection
### Quiz: JVM Memory Management and Garbage Collection
### Types of JVM Garbage Collectors
### Memory Leaks
## Collections


### Introduction
### Collections Class
### Collection Interface
### Quiz: Collection
### List Interface
### ArrayList
### LinkedList
### Quiz: List, ArrayList, LinkedList
### Set Interface
### HashSet
### TreeSet
### Quiz: Set and HashSet
### Queue Interface
### Priority Queue
### Deque Interface
### Map Interface
### HashMap
### Quiz: Queue and Map Interface
### Iterator
### Comparator Interface
### Comparable Interface
### Quiz: Iterators, Comparator vs Comparable
### Project: Face Detection System

## Lambda Expressions and Streams


### Lambda Expressions
### Method References
### Java Streams
### Quiz: Lambda Expressions and Streams
### To know Java 8 in detail, refer to - Java 8 Features
## Multithreading and Synchronization

### Introduction
### Threads
### Thread.start() vs Thread.run() Method
### Thread.sleep() Method
### Runnable Interface
### Quiz: Thread Basics and Lifecycle
### Main Thread
### Thread Priority in Multithreading
### Daemon Thread
### Quiz: Thread Methods and Daemon Threads
### Java Synchronization
### Quiz: Synchronization Basics
### Thread Safety
### Locks in Java
### Lock vs Monitor in Concurrency
### Lock Framework vs Thread Synchronization
### Reentrant Lock
### Deadlock in Multithreading
### Thread Pools
### Executor Framework
### Quiz: Deadlocks and Synchronization
### Project: Snake Game
## File Handling

### Introduction to Java IO
### Reader Class
### Writer Class
### File Handling
### File Class
### Quiz: File Handling
### FileInputStream
### FileOutputStream
### FileReader Class
### FileWriter Class
### FileOutput Stream
### BufferedReader Input Stream
### BufferedReader Output stream
### Fast I/O
### Quiz: File Writing
### FilePermission Class
### FileDescriptor Class
### Project: Text Editor
## Networking

### Introduction to Java Networking
### Quiz: Networking Basics and Protocols
### Socket Programming
### Server Socket Class
### Quiz: Sockets and Server Communication
### URL Class and Methods
### Project: Chat Application
### Java Database Connectivity(JDBC)
### Introduction to Java JDBC
### JDBC Driver
### JDBC Connection
### Types of Statements in JDBC
### Quiz: JDBC

## **(java 8)**

## 1. Lambda Expressions

### Introduction
### Lambda Expressions Parameters
### Java Lambda Expression with Collections
### Lambda Expression Variable Capturing
### Create a Thread using Lambda Expressions
### Serialization of Lambda Expression
### Block Lambda Expressions

## 2. Functional Interfaces


### Introduction
### Consumer Interface
### BiConsumer Interface
### Predicate Interface
### Function Interface
### Supplier Interface

## 3. Method Reference

### Introduction
### Method References
### Converting ArrayList to HashMap using Method Reference

## 4. Streams


### Introduction
### Implement Filter Function using Reduce
### Stream API Filters
### Parallel vs Sequential Stream
### Array to Stream
### Print Elements of a Stream
### Convert an Iterable to Stream
### Convert an Iterator to Stream
### Convert Stream to Set
### Convert a Set to Stream

## 5. Comparable and Comparator

### Comparable vs Comparator
### Comparator Interface
### Sort an Array of Triplet using Java Comparable and Comparator
### Sort LinkedList using Comparable
### Sort HashSet Elements using Comparable Interface
### Sort LinkedHashMap by Values using Comparable Interface
### Sort LinkedHashMap by Keys using Comparable Interface
## 6. Optional Class
### Introduction
### ofNullable() Method
### ifPresentOrElse() Method
### orElseGet() Method
### filter() Method
### hashCode() Method
### toString() Method
### equals() Method
### stream() Method
## 7. Date/Time API

### Introduction
### LocalDateTime Class
### MonthDay Class
### OffsetTime Class
### OffsetDateTime Class
### Clock Class
### ZonedDateTime Class
### ZoneOffset Class
### Year Class
### YearMonth Class
### Period Class
## 8. Other Java 8 Features

## 8.1 Java 8 Interface and Collection Enhancements
### Default Methods
### Static method
### Override Default Method
### forEach() method
### ArrayDeque removeIf() method
## 8.2 Functional Interfaces – Unary Operator
### LongUnaryOperator Interface
### IntUnaryOperator Interface
### DoubleUnaryOperator Interface
### UnaryOperator Interface
## 8.3 Functional Interfaces – Consumers and Suppliers
### LongConsumer Interface
### ObjLongConsumer Interface
### ObjIntConsumer Interface
### ObjDoubleConsumer Interface
### DoubleConsumer
### IntSupplier Interface
### BooleanSupplier Interface
### LongSupplier Interface
### DoubleSupplier Interface
## 8.4 Functional Interfaces – Functions and BiFunctions
### LongFunction Interface
### IntFunction Interface
### ToDoubleFunction Interface
### DoubleFunction Interface
### ToIntFunction Interface
### LongToIntFunction Interface
### ToLongFunction Interface
### LongToDoubleFunction Interface
### ToLongBiFunction Interface
### ToIntBiFunction Interface
### ToDoubleBiFunction Interface

## **(Springboot)**

## Spring Core Concept

### Inversion of Control
### Dependency Injection
### BeanFactory vs. ApplicationContext
### Spring Bean Lifecycle
### Singleton, Prototype Scope
### Custom Scope
### Create a Spring Bean
### Spring Autowiring
### DispatcherServlet
### Spring IoC Container
### Maven/Gradle (project build tools)
## Spring Boot Core Features


### Architecture
### Annotations
### Auto-configuration
### Spring Boot Starters
### Create a basic application
### Best Practices for Spring Boot Application
### Application Properties
### YAML Configuration
### Actuator
### Logging
### DevTools
## Spring Boot with REST API

### Introduction
### @RestController
### @RequestMapping
### @GetMapping & @PostMapping
### @PutMapping & @DeleteMapping
### @PathVariable & @RequestParam
### @RequestBody
### REST API
### JSON Serialization/Deserialization
### Exception Handling
### Validation
## Spring Boot with Database and Data JPA

### Integrating Spring Boot with MySQL
### PostgreSQL
### MongoDB
### Spring Data JPA
### Hibernate Basics
### JDBC
### CrudRepository vs. JpaRepository
### H2 Database for Testing
### CRUD Operations with JPA Repositories
### Project: Todo List API using Spring Boot and MySQL

## Advanced Spring Boot Features


### Scheduling Tasks
### Sending Emails
### File Handling & Uploading Files
### Caching
### Caching with other Providers
### Transaction Management
### DTO Mapping
## Microservices with Spring Boot

### Introduction
### Communication Between Spring Microservices
### Deploy Java Microservices on AWS Elastic Beanstalk
### Project: Microservices Sample Project
## Spring Boot with Kafka

### Kafka Producer and Consumer in Spring Boot
### Publishing and Consuming JSON Messages
### Publishing and Consuming String Messages
### Create and Configure Topics in Apache Kafka
### Consume Message Through Kafka, Save into ElasticSearch and Plot into Grafana
### Start/Stop a Kafka Listener Dynamically
## Spring Boot with AOP

### Introduction
### Spring Boot Advices
### Before
### After
### Around
### After Throwing
### After Returning
### AOP vs OOP
### AOP vs AspectJ
## Spring Boot Testing

### Unit Testing with JUnit
### Testing with Mockito
### Integration Testing with MockMVC
### Using ZeroCode for Testing
