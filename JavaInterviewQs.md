**Question 1: Java 8 features**

Java 8 introduced several powerful new features and enhancements that significantly changed the way Java programming is approached. Below are the main features of Java 8 along with explanations:

1. Lambda Expressions
Lambda expressions provide a clear and concise way to represent a method interface using an expression. They help in writing more readable and compact code, especially when used in collection operations.

Syntax Example:
```Java
// Before Java 8: Using an anonymous class
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello from Runnable");
    }
};

// Using Lambda Expression in Java 8
Runnable runnableLambda = () -> System.out.println("Hello from Lambda");

```

2. Functional Interfaces
Functional interfaces are interfaces with a single abstract method. They can be represented by lambda expressions. 
Java 8 introduced several built-in functional interfaces, such as Predicate, Function, Consumer, etc.

```Java
@FunctionalInterface
interface MyFunctionalInterface {
    void doSomething();
}

// Using Lambda Expression
MyFunctionalInterface action = () -> System.out.println("Doing something");
action.doSomething();
```

3. Stream API
The Stream API is used to process collections of data in a functional way. It allows operations like filtering, mapping, and reducing on collections.

```Java
List<String> names = Arrays.asList("John", "Jane", "Jack", "Jill");

// Filtering names that start with 'J' and converting to uppercase
names.stream()
     .filter(name -> name.startsWith("J"))
     .map(String::toUpperCase)
     .forEach(System.out::println);
```

4. Default and Static Methods in Interfaces
Java 8 allows interfaces to have default and static methods. Default methods provide a way to add new functionality to interfaces without breaking existing implementations.

```Java
interface MyInterface {
    void abstractMethod();

    // Default method
    default void defaultMethod() {
        System.out.println("This is a default method");
    }

    // Static method
    static void staticMethod() {
        System.out.println("This is a static method");
    }
}
```

5. Optional Class
The Optional class is used to represent optional values that may or may not be present. It helps to prevent NullPointerException.
```Java
Optional<String> optionalValue = Optional.ofNullable(null);

// Checking if value is present
if (optionalValue.isPresent()) {
    System.out.println(optionalValue.get());
} else {
    System.out.println("Value is not present");
}

// Using ifPresent() method
optionalValue.ifPresent(System.out::println);

```

6. New Date and Time API (java.time)
Java 8 introduced a new java.time package to replace the old java.util.Date and java.util.Calendar. The new API is more intuitive and provides better handling of date and time.
```Java
LocalDate today = LocalDate.now();
LocalDate birthDate = LocalDate.of(1990, Month.APRIL, 15);

Period age = Period.between(birthDate, today);
System.out.println("Age: " + age.getYears() + " years");

```

7. Method References
Method references are used to refer to a method without executing it. They are a shorthand notation of a lambda expression that only calls an existing method.
```Java
List<String> names = Arrays.asList("John", "Jane", "Jack");

// Using lambda expression
names.forEach(name -> System.out.println(name));

// Using method reference
names.forEach(System.out::println);

```

8. Collectors Class
The Collectors class is part of the java.util.stream package and is used to collect elements from a stream and store them in different types of results, such as lists, sets, or maps.
```Java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Collecting names that start with 'A' into a list
List<String> filteredNames = names.stream()
                                   .filter(name -> name.startsWith("A"))
                                   .collect(Collectors.toList());
System.out.println(filteredNames);

```

9. Parallel Streams
Java 8 introduced parallel streams, allowing data processing to be performed in parallel, taking advantage of multi-core processors.
```Java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Using parallel stream to compute the sum
int sum = numbers.parallelStream()
                 .reduce(0, Integer::sum);
System.out.println("Sum: " + sum);

```


**Question 2:- What are inbuilt methods of functional interfaces**

Java's functional interfaces come with a variety of inbuilt methods that can be leveraged to perform common operations. These interfaces are part of the java.util.function package, which includes a set of standard functional interfaces like Predicate, Function, Consumer, Supplier, etc. Below is a list of common functional interfaces along with their inbuilt methods:

Java's functional interfaces come with a variety of inbuilt methods that can be leveraged to perform common operations. These interfaces are part of the `java.util.function` package, which includes a set of standard functional interfaces like `Predicate`, `Function`, `Consumer`, `Supplier`, etc. Below is a list of common functional interfaces along with their inbuilt methods:

### 1. **Predicate<T>**
Represents a condition (boolean-valued function) of one argument.

- **`test(T t)`**: Evaluates the predicate (condition) on the given argument.
```Java
Predicate<String> isEmpty = String::isEmpty;
boolean result = isEmpty.test(""); // true
```

- **`and(Predicate<? super T> other)`**: Returns a composed predicate that represents a short-circuiting logical AND of this predicate and another.
```Java
Predicate<String> isNotEmpty = isEmpty.negate();
```

- **`or(Predicate<? super T> other)`**: Returns a composed predicate that represents a short-circuiting logical OR of this predicate and another.

- **`negate()`**: Returns a predicate that represents the logical negation of this predicate.

### 2. **Function<T, R>**
Represents a function that accepts one argument and produces a result.

- **`apply(T t)`**: Applies this function to the given argument.
```Java
Function<String, Integer> lengthFunction = String::length;
int length = lengthFunction.apply("Hello"); // 5
```

- **`andThen(Function<? super R, ? extends V> after)`**: Returns a composed function that first applies this function and then applies the `after` function.

- **`compose(Function<? super V, ? extends T> before)`**: Returns a composed function that first applies the `before` function and then applies this function.

### 3. **Consumer<T>**
Represents an operation that accepts a single argument and returns no result.

- **`accept(T t)`**: Performs the operation on the given argument.
```Java
Consumer<String> printConsumer = System.out::println;
printConsumer.accept("Hello"); // Prints "Hello"
```

- **`andThen(Consumer<? super T> after)`**: Returns a composed `Consumer` that performs, in sequence, this operation followed by the `after` operation.

### 4. **Supplier<T>**
Represents a supplier of results.

- **`get()`**: Gets a result.
```Java
Supplier<String> supplier = () -> "Hello, World!";
String result = supplier.get(); // "Hello, World!"
```

### 5. **UnaryOperator<T>**
A specialized `Function` that takes one argument and returns a result of the same type.

- **`apply(T t)`**: Applies the operation to the given argument.
```Java
UnaryOperator<Integer> square = x -> x * x;
int result = square.apply(5); // 25
```

### 6. **BinaryOperator<T>**
A specialized `BiFunction` that takes two arguments of the same type and returns a result of the same type.

- **`apply(T t1, T t2)`**: Applies the operation to the given arguments.
```Java
BinaryOperator<Integer> sum = (a, b) -> a + b;
int result = sum.apply(3, 4); // 7
```

### 7. **BiFunction<T, U, R>**
Represents a function that accepts two arguments and produces a result.

- **`apply(T t, U u)`**: Applies the function to the given arguments.
```Java
BiFunction<Integer, Integer, Integer> multiply = (a, b) -> a * b;
int result = multiply.apply(3, 4); // 12
```

### 8. **BiConsumer<T, U>**
Represents an operation that accepts two arguments and returns no result.

- **`accept(T t, U u)`**: Performs the operation on the given arguments.
```Java
BiConsumer<String, Integer> printNameAndAge = (name, age) -> System.out.println(name + " is " + age + " years old");
printNameAndAge.accept("John", 25); // "John is 25 years old"
```

### 9. **BiPredicate<T, U>**
Represents a condition that accepts two arguments and returns a boolean result.

- **`test(T t, U u)`**: Evaluates the predicate on the given arguments.
```Java
BiPredicate<String, String> areEqual = String::equals;
boolean result = areEqual.test("test", "test"); // true
```



**Question 3:- Predicate vs Function**

## Predicate vs Function

In Java 8, `Predicate` and `Function` are two commonly used functional interfaces that serve different purposes. Below is a comparison of both:

### 1. **Predicate<T>**
- **Purpose:** Represents a boolean-valued function of one argument.
- **Method:** 
  - `boolean test(T t)`: Evaluates the predicate on the given argument.

#### Example:
```Java
Predicate<String> isEmpty = String::isEmpty;
boolean result = isEmpty.test(""); // true
```

- **Composing Predicates:**
  - `Predicate<T> and(Predicate<? super T> other)`: Returns a composed predicate that represents a short-circuiting logical AND.
  - `Predicate<T> or(Predicate<? super T> other)`: Returns a composed predicate that represents a short-circuiting logical OR.
  - `Predicate<T> negate()`: Returns a predicate that represents the logical negation of this predicate.

### 2. **Function<T, R>**
- **Purpose:** Represents a function that accepts one argument and produces a result.
- **Methods:**
  - `R apply(T t)`: Applies this function to the given argument.

#### Example:
```Java
Function<String, Integer> lengthFunction = String::length;
int length = lengthFunction.apply("Hello"); // 5
```

- **Composing Functions:**
  - `Function<T, V> andThen(Function<? super R, ? extends V> after)`: Returns a composed function that first applies this function and then applies the after function.
  - `Function<T, V> compose(Function<? super V, ? extends T> before)`: Returns a composed function that first applies the before function and then applies this function.

### Summary
- Use **Predicate** when you want to evaluate a condition (returning a boolean).
- Use **Function** when you want to transform or map an input to an output.


**Question 4- Create predicate to check if number is even**
## Create a Predicate to Check if a Number is Even

In Java, you can use a `Predicate` to evaluate whether a number is even. Below is an example:

### Example:
```Java
import java.util.function.Predicate;

public class EvenNumberCheck {
    public static void main(String[] args) {
        Predicate<Integer> isEven = number -> number % 2 == 0;

        // Test the predicate
        System.out.println(isEven.test(4)); // true
        System.out.println(isEven.test(7)); // false
    }
}
```

### Explanation:
- **Predicate Definition:** 
  - The `isEven` predicate takes an `Integer` as input and returns `true` if the number is even (i.e., the remainder when divided by 2 is zero).
  
- **Testing the Predicate:**
  - The `test` method is used to evaluate the predicate for different numbers.


**Question 5- When and why abstraction exists in class and methods**
## When and Why Abstraction Exists in Classes and Methods in Java

Abstraction is a core concept in object-oriented programming (OOP) that focuses on exposing only the essential features of an object while hiding the implementation details. In Java, abstraction can be achieved using abstract classes and interfaces.

### When Abstraction Exists
1. **Abstract Classes**:
   - Used when you want to provide a common base for a group of related classes while still allowing for flexibility in implementation.
   - An abstract class can have both abstract methods (without a body) and concrete methods (with a body).
   - Example: A `Shape` class can be abstract with an abstract method `draw()`, allowing different shapes (like `Circle`, `Rectangle`) to implement their own version of `draw()`.

2. **Interfaces**:
   - Used when you want to define a contract that other classes must adhere to without dictating how they should be implemented.
   - An interface can contain only method signatures (abstract methods) and constants. From Java 8 onwards, it can also have default and static methods.
   - Example: An interface `Animal` can define a method `makeSound()`, which all animal classes (like `Dog`, `Cat`) must implement.

### Why Abstraction Exists
1. **Encapsulation of Complexity**:
   - By hiding the complex implementation details and exposing only the necessary parts, abstraction simplifies the interaction with objects.
   - This leads to easier understanding and usage of classes and methods.

2. **Code Reusability**:
   - Abstraction promotes code reusability by allowing developers to define methods in an abstract class or interface, which can be implemented by multiple subclasses.

3. **Maintainability**:
   - Changes to the implementation of abstract methods do not affect the classes that use them, making the codebase easier to maintain and update.

4. **Flexibility and Extensibility**:
   - New classes can be created to extend or implement abstract classes or interfaces without modifying existing code, promoting flexibility and extensibility in software design.

### Summary
- Abstraction exists in Java classes and methods to encapsulate complexity, enhance code reusability, maintainability, and provide flexibility in design.



**Question 6- What is base class of exception**
## What is the Base Class of Exception in Java?

In Java, the base class for all exceptions is the `Throwable` class. It serves as the superclass for all error and exception classes in Java. The `Throwable` class is found in the `java.lang` package.

### Hierarchy of Exception Classes

1. **Throwable**:
   - The root class for all errors and exceptions.
   - Has two primary subclasses:
     - **Error**: Represents serious problems that a reasonable application should not try to catch. Errors are typically not recoverable. For example, `OutOfMemoryError` and `StackOverflowError`.
     - **Exception**: Represents conditions that a reasonable application might want to catch. This class is further divided into checked exceptions and unchecked exceptions.

2. **Exception**:
   - Subclass of `Throwable`.
   - Checked exceptions (e.g., `IOException`, `SQLException`): Must be either caught or declared in the method signature using the `throws` keyword.
  


## Question 6- HashMap Internal Working in Java

A `HashMap` in Java is a part of the Java Collections Framework and implements the `Map` interface. It is used to store key-value pairs and provides efficient insertion, deletion, and retrieval operations.

### Internal Structure

1. **Array of Buckets**:
   - A `HashMap` uses an array to store its entries, where each entry is a bucket that can contain multiple key-value pairs.
   - The initial capacity of the array is specified at the time of creation, and it can dynamically grow when the number of entries exceeds a certain threshold (load factor).

2. **Hash Function**:
   - Each key is processed through a hash function to compute its hash code.
   - The hash code is then transformed into an index that determines which bucket the key-value pair will be stored in.
   - The default hash function is based on the `hashCode()` method of the key object.

3. **Collision Handling**:
   - When two keys hash to the same bucket index (a collision), the `HashMap` handles it using a linked list or, in Java 8 and later, a balanced tree (Red-Black tree) if the number of collisions exceeds a certain threshold (8 by default).
   - This means that each bucket can contain multiple entries, allowing the `HashMap` to store multiple key-value pairs with different keys but the same hash code.

### Key Operations

1. **Insertion**:
   - When a new key-value pair is added, the hash code of the key is computed, and the index of the bucket is determined.
   - If the bucket is empty, the key-value pair is added directly.
   - If the bucket already contains entries, the `HashMap` checks for existing keys. If the key exists, its value is updated; otherwise, the new entry is added to the bucket.

2. **Retrieval**:
   - To retrieve a value, the hash code of the key is calculated, and the corresponding bucket is located.
   - The `HashMap` then iterates through the entries in that bucket to find the key and return the associated value.

3. **Deletion**:
   - Similar to retrieval, the hash code is computed, and the corresponding bucket is located.
   - The `HashMap` searches for the key in the bucket and removes the key-value pair if found.

### Load Factor and Rehashing

- The load factor is a measure of how full the `HashMap` can get before it needs to resize. The default load factor is 0.75, meaning that when the number of entries exceeds 75% of the current capacity, the `HashMap` is resized.
- Resizing involves creating a new array with double the capacity and rehashing all existing entries to the new buckets based on their hash codes.

### Summary

- A `HashMap` in Java uses an array of buckets to store key-value pairs, utilizing a hash function to determine the index for each key.
- It handles collisions using linked lists or trees and dynamically resizes based on load factor.
- This structure allows for efficient average-case time complexity for insertion, deletion, and retrieval operations, typically O(1).


## Question 7- Internal Working of HashMap `put` Method

The `put` method in a `HashMap` is used to insert key-value pairs into the map. Here's how it works internally:

### Step-by-Step Process

1. **Calculate Hash Code**:
   - When the `put` method is called with a key-value pair, the first step is to calculate the hash code of the key using the `hashCode()` method.
   - This hash code is then processed to get an index for the array (buckets) where the entry should be stored.

   ```java
   int hash = key.hashCode();
   int index = hash % capacity; // capacity is the size of the bucket array
   ```

2. **Locate Bucket**:
   - The index computed is used to locate the appropriate bucket in the internal array of the `HashMap`.

3. **Check for Existing Entries**:
   - If the bucket at the computed index is empty, the new key-value pair is added directly.
   - If there are existing entries in the bucket (due to hash collisions), the `HashMap` checks each entry:
     - If an entry with the same key is found, the associated value is updated with the new value.
     - If no entry with the same key is found, the new entry is appended to the bucket.

   ```java
   // If bucket is empty, create a new Entry
   if (bucket == null) {
       bucket = new Entry(key, value);
       buckets[index] = bucket; // Add to the array
   } else {
       // Traverse the linked list or tree structure to find the key
       for (Entry entry


## Question 8- What is Hash Collision?

A **hash collision** occurs when two different keys produce the same hash code when passed through a hash function. In the context of data structures like `HashMap`, this means that two distinct keys are mapped to the same index in the underlying array (buckets).

### How Hash Collisions Happen

- Hash functions are designed to distribute keys uniformly across the available indices. However, due to the finite size of the hash table and the potentially infinite number of keys, it is inevitable that some keys will hash to the same index.
  
- For example, consider a simple hash function that uses the modulo operator:

  ```java
  int hashCode = key.hashCode();
  int index = hashCode % capacity; // capacity is the size of the bucket array
  ```

  If two different keys, `key1` and `key2`, have hash codes such that:

  ```
  key1.hashCode() % capacity == key2.hashCode() % capacity
  ```

  Then both keys will map to the same index, resulting in a collision.

### Handling Hash Collisions

`HashMap` uses several techniques to handle collisions:

1. **Chaining**:
   - Each index in the hash table contains a linked list (or tree structure) of entries. When a collision occurs, the new entry is added to the list at that index.

   ```java
   // Pseudocode for chaining
   if (buckets[index] == null) {
       buckets[index] = new Entry(key, value);
   } else {
       // Traverse the linked list to find the key or append new entry
   }
   ```

2. **Open Addressing**:
   - In this approach, if a collision occurs, the algorithm looks for the next available index in the array (linear probing, quadratic probing, or double hashing) until it finds an empty slot.

### Example of a Hash Collision

```java
// Assuming a simple hash function and a small bucket array size
int capacity = 10;
int key1 = 12;
int key2 = 22;

int index1 = key1 % capacity;
```

 
## Question 8- What is a Load Factor?

The **load factor** is a measure used in hash-based data structures, such as `HashMap`, to determine how full the data structure is. It is defined as the ratio of the number of entries (key-value pairs) to the total number of buckets (or slots) in the hash table.

### Formula

The load factor can be calculated using the following formula:

```
Load Factor = Number of Entries / Number of Buckets
```

### Significance of Load Factor

1. **Performance**:
   - A higher load factor means that the hash table is more filled, which can lead to more hash collisions and consequently longer lookup times. 
   - A lower load factor indicates more empty buckets, which generally leads to better performance as there are fewer collisions.

2. **Resizing**:
   - In most hash table implementations, such as `HashMap`, a threshold is set for the load factor (commonly 0.75). When the load factor exceeds this threshold, the hash table is resized (usually doubled in size), and all existing entries are rehashed into the new buckets. 
   - This resizing process helps maintain efficient performance by keeping the load factor within a reasonable range.

### Example

Suppose we have a `HashMap` with a capacity of 10 (10 buckets) and currently holds 7 entries. The load factor would be calculated as follows:

```java
int numberOfEntries = 7;
int numberOfBuckets = 10;

double loadFactor = (double) numberOfEntries / numberOfBuckets; // 0.7
```

### Conclusion

The load factor is an important aspect of hash tables, as it affects both performance and memory usage. Understanding how the load factor


## Question- @SpringBootApplication

## SpringBootApplication Annotation

The `@SpringBootApplication` annotation is a convenience annotation that combines three important annotations in Spring Boot. It serves as a central configuration annotation for Spring Boot applications.

### Components of @SpringBootApplication

1. **@Configuration**:
   - Indicates that the class can be used by the Spring IoC (Inversion of Control) container as a source of bean definitions. It allows you to define beans using the `@Bean` annotation.

2. **@EnableAutoConfiguration**:
   - Enables Spring Boot's auto-configuration mechanism. This automatically configures your Spring application based on the dependencies present on the classpath. For example, if you have `spring-boot-starter-web` on the classpath, it will automatically configure a web server.

3. **@ComponentScan**:
   - Instructs Spring to scan the current package and its sub-packages for components, configurations, and services. This is where Spring looks for classes annotated with `@Component`, `@Service`, `@Repository`, etc.

### Usage

To use the `@SpringBootApplication` annotation, simply place it on your main application class. Here’s an example:

```Java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

### Benefits

- **Simplicity**: Reduces boilerplate code by consolidating multiple annotations into one.
- **Convention over Configuration**: Promotes a default setup, making it easier to get started with Spring Boot.
- **Ease of Use**: Makes it straightforward to create and configure a Spring application.

### Conclusion

The `@SpringBootApplication` annotation is a powerful and essential feature in Spring Boot that simplifies the configuration and setup of Spring applications, allowing developers to focus on building features rather than managing boilerplate code.



**Question- Starting point of Springboot application**

## Starting Point of a Spring Boot Application

The starting point of a Spring Boot application is the class that contains the `main` method, which is typically annotated with `@SpringBootApplication`.

### Components

1. **Main Class with `@SpringBootApplication` Annotation**:
   - This class serves as the entry point for the entire Spring Boot application.
   - The `@SpringBootApplication` annotation combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan` to configure and bootstrap the application.

2. **`SpringApplication.run()` Method**:
   - The `main` method uses the `SpringApplication.run()` method to launch the application. This method starts the Spring application context and the embedded server (e.g., Tomcat) if it is a web application.
   - It also triggers the auto-configuration and scans the classpath for components to register as beans.

### Example

```Java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        // Starting point of the Spring Boot application
        SpringApplication.run(MyApplication.class, args);
    }
}
```

### Explanation

- **`main(String[] args)`**:
  - The `main` method is the standard Java entry point for an application.
  - `SpringApplication.run()` is used to bootstrap the application, which starts the Spring context and the embedded web server.

- **How it Works**:
  - When `SpringApplication.run()` is called, it creates an instance of `SpringApplication`, loads the application context, and performs the necessary auto-configuration based on the classpath.

### Flow of Execution

1. **Bootstrap**: The `main` method is executed, which then calls `SpringApplication.run()`.
2. **Context Initialization**: Spring Boot creates and initializes the application context (Spring IoC container).
3. **Component Scanning and Bean Creation**: Beans are created, dependencies are injected, and the auto-configuration kicks in to provide configurations for components like databases, web servers, etc.
4. **Embedded Server Startup**: For web applications, an embedded web server like Tomcat or Jetty is started.
5. **Application Ready**: After all configurations are done, the application is ready to handle requests or perform its intended operations.

### Conclusion

The starting point of a Spring Boot application is the main class with the `main` method. The `SpringApplication.run()` method plays a crucial role in bootstrapping the Spring Boot environment and starting the application.



## Question `@Component` vs `@Bean` vs `@Configuration`

### 1. `@Component`
- `@Component` is a class-level annotation that is used to mark a class as a Spring-managed component.
- Spring automatically detects classes annotated with `@Component` during component scanning and registers them as beans in the Spring application context.
- It is part of the Spring stereotype annotations, which include `@Service`, `@Repository`, and `@Controller`, each serving a specific purpose but essentially working the same way as `@Component`.

**Example**:
```Java
import org.springframework.stereotype.Component;

@Component
public class MyComponent {
    public void sayHello() {
        System.out.println("Hello from MyComponent!");
    }
}
```

### 2. `@Bean`
- `@Bean` is a method-level annotation that is used to define a bean explicitly in the Spring configuration.
- It is typically used in a method annotated with `@Configuration` to create and manage beans that are not easily amenable to component scanning, such as third-party classes.
- The method annotated with `@Bean` returns an instance of the bean that will be managed by Spring.

**Example**:
```Java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public MyComponent myComponent() {
        return new MyComponent(); // MyComponent bean managed by Spring
    }
}
```

### 3. `@Configuration`
- `@Configuration` is a class-level annotation that is used to indicate that the class can be used as a source of bean definitions.
- Classes annotated with `@Configuration` are used to define Spring beans using the `@Bean` annotation.
- It indicates that the class is a Spring configuration class, and its methods can be used to define and configure beans.

**Example**:
```Java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public MyComponent myComponent() {
        return new MyComponent(); // MyComponent bean managed by Spring
    }
}
```

### Differences

| Annotation      | Level       | Purpose                                                               | Usage Example                          |
|-----------------|-------------|-----------------------------------------------------------------------|----------------------------------------|
| `@Component`    | Class       | To mark a class as a Spring-managed component, discovered via scanning. | Used for general-purpose beans like services or repositories. |
| `@Bean`         | Method      | To explicitly define a bean to be managed by the Spring container.    | Used when third-party or custom instantiation logic is required. |
| `@Configuration`| Class       | To declare that a class provides Spring configuration.                | Used to create a centralized configuration for beans. |

### Use Cases

- **`@Component`**:
  - Use it when you have classes under your control that are part of the core application logic and can be easily discovered via component scanning.
- **`@Bean`**:
  - Use it when you need to manually create beans, such as for third-party library classes or when instantiation requires custom logic.
- **`@Configuration`**:
  - Use it to define a class that declares one or more `@Bean` methods, which can be centralized in a configuration class to manage beans efficiently.

### Example Comparison

```Java
// Using @Component
@Component
public class MyService {
    // service code
}

// Using @Configuration and @Bean
@Configuration
public class AppConfig {
    
    @Bean
    public MyService myService() {
        return new MyService(); // MyService bean managed by Spring
    }
}
```

In the above examples, the `@Component` approach automatically registers the class, whereas `@Bean` is used in a configuration class to manually define the bean.


**Question -**

## `@Qualifier` with Bean Type

### Overview
- `@Qualifier` is an annotation in Spring used to differentiate between multiple beans of the same type.
- When more than one bean of the same type is present in the Spring application context, `@Qualifier` can be used to specify which one should be injected.
- It is used in conjunction with `@Autowired` to avoid ambiguity during dependency injection.

### Example Scenario
Suppose you have two implementations of an interface `Vehicle` and you want to decide which implementation to inject into a class.

```Java
public interface Vehicle {
    void start();
}

@Component
public class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car started");
    }
}

@Component
public class Bike implements Vehicle {
    @Override
    public void start() {
        System.out.println("Bike started");
    }
}
```

If you use `@Autowired` without `@Qualifier`, Spring will not know whether to inject `Car` or `Bike` because both implement the `Vehicle` interface.

```Java
@Component
public class VehicleService {

    private final Vehicle vehicle;

    @Autowired
    public VehicleService(Vehicle vehicle) {
        this.vehicle = vehicle; // Ambiguity here - which Vehicle to inject?
    }

    public void useVehicle() {
        vehicle.start();
    }
}
```

### Using `@Qualifier`
To specify which implementation to inject, use `@Qualifier`:

```Java
@Component
public class VehicleService {

    private final Vehicle vehicle;

    @Autowired
    public VehicleService(@Qualifier("car") Vehicle vehicle) {
        this.vehicle = vehicle; // Explicitly inject the Car implementation
    }

    public void useVehicle() {
        vehicle.start();
    }
}
```

In this example, `@Qualifier("car")` tells Spring to inject the `Car` bean. The bean name (e.g., `"car"`) matches the class name by default (with the first letter in lowercase) unless explicitly specified otherwise.

### Example with Method-Level `@Bean`
You can also use `@Qualifier` with beans defined using `@Bean` in a configuration class.

```Java
@Configuration
public class AppConfig {

    @Bean
    public Vehicle car() {
        return new Car();
    }

    @Bean
    public Vehicle bike() {
        return new Bike();
    }
}

@Component
public class VehicleService {

    private final Vehicle vehicle;

    @Autowired
    public VehicleService(@Qualifier("bike") Vehicle vehicle) {
        this.vehicle = vehicle; // Explicitly inject the Bike bean
    }

    public void useVehicle() {
        vehicle.start();
    }
}
```

### Summary
- `@Qualifier` is useful when multiple beans of the same type are present, and you need to specify which one to inject.
- It works with both `@Component`-scanned beans and `@Bean`-defined beans.
- Always use the bean name specified in the `@Qualifier` to avoid ambiguity.


### Question SQL Query: Find Employees Who Are Managers and Belong to a Different Department Than the One They Manage

#### **Question:**
You are given two tables: `Employees` and `Departments`. Write a query to find all employees who are **managers** and belong to a **different department** than the one they manage.

#### **Schema Example:**

1. **`Employees` Table**:

| employee_id | employee_name | department_id | manager_id |
|-------------|---------------|---------------|------------|
| 1           | Alice         | 10            | NULL       |
| 2           | Bob           | 20            | 1          |
| 3           | Charlie       | 10            | 1          |
| 4           | David         | 30            | NULL       |
| 5           | Eve           | 40            | 4          |
| 6           | Frank         | 50            | 4          |
| 7           | Grace         | 30            | 5          |

- **employee_id**: Unique ID for each employee.
- **department_id**: The department the employee belongs to.
- **manager_id**: The ID of the employee’s manager (NULL if the employee is a manager).

2. **`Departments` Table**:

| department_id | department_name | manager_id |
|---------------|-----------------|------------|
| 10            | Sales           | 1          |
| 20            | Marketing       | 3          |
| 30            | IT              | 5          |
| 40            | HR              | 4          |
| 50            | R&D             | 6          |

- **department_id**: Unique ID for each department.
- **manager_id**: The ID of the employee who manages the department.

#### **SQL Query:**

```sql
SELECT e.employee_id, e.employee_name, e.department_id AS employee_department, d.department_id AS managed_department
FROM Employees e
JOIN Departments d ON e.employee_id = d.manager_id
WHERE e.department_id != d.department_id;
```


### SQL Query: Fetch the Second Highest Salary Employee

#### **Question:**
Write a SQL query to retrieve the **second-highest salary** employee from the `Employees` table.

#### **Schema Example:**

| employee_id | employee_name | salary |
|-------------|---------------|--------|
| 1           | Alice         | 100000 |
| 2           | Bob           | 80000  |
| 3           | Charlie       | 120000 |
| 4           | David         | 90000  |
| 5           | Eve           | 120000 |

#### **Approach 1: Using a Subquery**

This approach uses a subquery to find the second-highest salary by first finding the maximum salary and then looking for the next maximum value that is less than it.

```sql
SELECT employee_name, salary
FROM Employees
WHERE salary = (
    SELECT MAX(salary) 
    FROM Employees 
    WHERE salary < (SELECT MAX(salary) FROM Employees)
);
```


