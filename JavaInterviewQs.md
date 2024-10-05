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

**Question:- Implement a rate limiter to limit number of requests made to an endpoint.**

# Rate Limiter Setup and Working

In this example, you are using **Bucket4j**, a token-bucket-based library, to implement rate limiting. Here's how the rate limiter works in conjunction with the Employee API. 

[GitHub link for code](https://github.com/deveshyadav/interview_prep/tree/master)

## Token Bucket Concept:

- A bucket holds tokens. Each API request consumes one token.
- When a request comes in, the rate limiter checks if there are tokens available in the bucket.
- If a token is available, it is consumed, and the request is allowed.
- If no token is available, the request is denied, and the user gets an HTTP 429 **Too Many Requests** error.
- Tokens refill into the bucket at a set rate, allowing requests again after a period.

## Rate Limiter Configuration:

- The rate limiter is set up in the `RateLimiterService` class using Bucket4j's API.
- You configure how many requests are allowed per time period. For example:
  - **20 requests per minute**: The bucket starts with 20 tokens and refills at a rate of 20 tokens every minute.

## Working Flow (Step-by-Step):

### Client Sends Request:

- A client (Postman, browser, etc.) sends a request to the `GET /employee/{id}` API.

### Rate Limiter Checks the Token Bucket:

- The `RateLimiterService.isRequestAllowed()` method is called when the request is received.
- Inside this method, the Bucket (configured with 20 tokens and refilling 20 tokens per minute) checks if there's a token available for this request.
  - **If token is available**: The token is consumed, and the request is processed.
  - **If no token is available**: The request is rejected, and a **429 Too Many Requests** response is sent.

### Processing the Request (If Allowed):

- If the request is allowed, the `EmployeeService` fetches the employee information based on the `id` parameter.
- The API returns the employee details in the response with a **200 OK** status.

### Rejecting the Request (If Rate Limited):

- If no token is available (because the rate limit has been exceeded), the response is set to **429 Too Many Requests**.
- No further processing occurs, and the client is informed to retry later.



**Question- Java memory working in case of object creation**

# Java Memory Management

## 1. Memory Areas in Java
Java memory is divided into several areas:

- **Heap Memory**: This is where all Java objects and arrays are allocated. The heap is created when the Java Virtual Machine (JVM) starts and can grow and shrink as needed. The memory for objects is allocated on the heap when you create an object using the `new` keyword.

- **Stack Memory**: Each thread in Java has its own stack, which is used to store local variables and method call frames. When a method is called, a new frame is pushed onto the stack containing parameters and local variables, including references to objects. When the method exits, the frame is popped from the stack.

- **Method Area**: This is a part of the heap memory where class structures (like metadata, constant pool, and field and method data) are stored. It holds the class definitions and is shared among all threads.

- **Native Method Stack**: This is similar to the stack but is used for native (non-Java) methods.

## 2. Object Creation Process
When you create an object in Java, the following steps occur:

### a. Memory Allocation
- **Using the `new` Keyword**: When you create an object using the `new` keyword, the JVM allocates memory for the object in the heap.

```java
MyObject obj = new MyObject();
```
## Memory Size
The amount of memory allocated depends on the object’s class and its instance variables.

### b. Constructor Invocation
After memory allocation, the constructor of the class is invoked to initialize the object. The constructor can also set initial values for the object’s fields.

### c. Object Reference
A reference to the newly created object is returned. In the example above, `obj` holds a reference to the memory location of the object.

### d. Garbage Collection
When an object is no longer referenced (i.e., there are no more references pointing to it), it becomes eligible for garbage collection. The JVM automatically reclaims memory used by objects that are no longer in use. This helps manage memory and prevent memory leaks.

## 3. Memory Management Mechanisms
- **Garbage Collection**: Java uses a garbage collection mechanism to automatically manage memory. This process identifies and disposes of objects that are no longer referenced, freeing up memory.

- **Generational Garbage Collection**: Java employs a generational garbage collection strategy where the heap is divided into generations (young, old, and permanent). New objects are allocated in the young generation, and as they survive garbage collection cycles, they are moved to older generations.

- **Finalization**: Before an object is garbage collected, the JVM can call its `finalize()` method (if it exists) to allow the object to release resources.



**Question- Java memory working in case of String literals and objects**
# Memory Utilization of Strings in Java

## 1. String Creation
- **String Literal**: 
  - Created with `String s = "Hello";` 
  - Stored in the **String Pool**, which allows reusing existing instances for the same literals.
  
- **String Object**: 
  - Created with `new String("Hello");` 
  - Allocates a new object in heap memory, bypassing the String Pool.

## 2. Memory Overhead
- Each string object has a header and consumes memory as follows:
  \[
  \text{Memory Used} = 24 + 2 \times n
  \]
  where \(n\) is the number of characters. The overhead is due to object metadata.

## 3. Immutability
- Strings are immutable. Modifying a string creates a new object, leading to increased memory usage. 
  - For example:
    ```java
    String s = "Hello";
    s += " World"; // Creates a new string object
    ```

## 4. Memory Management
- Java uses garbage collection to reclaim memory from unreferenced string objects. Frequent string modifications can trigger more garbage collection cycles.

## 5. Using StringBuilder/StringBuffer
- For frequent modifications, use `StringBuilder` or `StringBuffer`:
  ```java
  StringBuilder sb = new StringBuilder("Hello");
  sb.append(" World");

  ```
  


  **Question**
# Serialization vs. Deserialization

## Serialization
- **Definition**: The process of converting an object into a byte stream.
- **Purpose**: To save the state of an object to a file or transmit it over a network.
- **Use Cases**: Storing objects in files, sending objects between systems, caching objects.
- **Example**:
    ```java
    ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("file.ser"));
    out.writeObject(object);
    out.close();
    ```

## Deserialization
- **Definition**: The process of converting a byte stream back into an object.
- **Purpose**: To reconstruct an object from its saved state.
- **Use Cases**: Retrieving objects from files, receiving objects over a network, restoring application state.
- **Example**:
    ```java
    ObjectInputStream in = new ObjectInputStream(new FileInputStream("file.ser"));
    MyObject object = (MyObject) in.readObject();
    in.close();
    ```

## Summary
- **Serialization**: Object → Byte Stream
- **Deserialization**: Byte Stream → Object


# Question- Integrating SonarQube with a Java Spring Boot Project

## Prerequisites
- **SonarQube Server**: Ensure that you have a running SonarQube server.
- **SonarQube Scanner**: Install SonarQube Scanner on your local machine or CI/CD pipeline.

## Steps to Integrate

### 1. Add SonarQube Dependency
Add the SonarQube plugin in your `pom.xml` file for Maven projects:

```xml
<properties>
    <sonar.version>your-sonar-version</sonar.version>
</properties>

<build>
    <plugins>
        <plugin>
            <groupId>org.sonarsource.scanner.maven</groupId>
            <artifactId>sonar-maven-plugin</artifactId>
            <version>${sonar.version}</version>
        </plugin>
    </plugins>
</build>
```


 **Properties**

sonar.projectKey=your-project-key
sonar.projectName=Your Project Name
sonar.projectVersion=1.0
sonar.sources=src/main/java
sonar.tests=src/test/java
sonar.java.binaries=target/classes



# Question- ECS Deployment Process

## Overview
Amazon ECS is a fully managed container orchestration service that helps deploy and manage Docker containers. The deployment process involves several key steps.

## Steps to Deploy on ECS

### 1. **Create a Docker Image**
- Build your application as a Docker container.
- Use a Dockerfile to define the environment and application dependencies.
- Build the Docker image using the command:
    ```bash
    docker build -t your-image-name .
    ```

### 2. **Push Docker Image to Amazon ECR**
- Create an Amazon ECR (Elastic Container Registry) repository to store your Docker images.
- Authenticate Docker to your ECR:
    ```bash
    aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-region.amazonaws.com
    ```
- Tag your image and push it to ECR:
    ```bash
    docker tag your-image-name:latest your-account-id.dkr.ecr.your-region.amazonaws.com/your-repo-name:latest
    docker push your-account-id.dkr.ecr.your-region.amazonaws.com/your-repo-name:latest
    ```

### 3. **Create ECS Cluster**
- Go to the ECS console and create a new cluster (EC2 or Fargate).
- Configure cluster settings based on your requirements.

### 4. **Define a Task Definition**
- Create a task definition that specifies:
  - The Docker image to use.
  - CPU and memory requirements.
  - Networking mode and port mappings.
  - Environment variables and IAM roles.

### 5. **Deploy the Service**
- Create a new service in your ECS cluster using the task definition.
- Choose the desired number of tasks to run and deployment options (e.g., rolling updates).
- Select the load balancer if needed (for web applications).

### 6. **Monitor and Manage**
- Use the ECS console to monitor the status of your tasks and services.
- Update the service with a new task definition version to deploy updates.

## Summary
Deploying on Amazon ECS involves creating a Docker image, pushing it to ECR, defining a task, and creating a service to manage the containers. ECS automates scaling, load balancing, and orchestration.




# Question- Handling Security Vulnerabilities with Black Duck

## Overview
Black Duck is an open-source management tool that helps identify security vulnerabilities in your code and dependencies. It scans your project and provides detailed insights into potential risks.

## Steps for Handling Vulnerabilities

### 1. **Integration**
- Integrate Black Duck into your CI/CD pipeline to automate scanning.
- Black Duck supports various build tools and environments (e.g., Maven, Gradle, Jenkins).

### 2. **Code Scanning**
- Run a Black Duck scan on your project to analyze the codebase and its dependencies.
- The scan identifies open-source components and versions in use.

### 3. **Vulnerability Detection**
- Black Duck checks the identified components against its comprehensive vulnerability database.
- It identifies known vulnerabilities (CVEs) and provides severity ratings.

### 4. **Reporting**
- After the scan, Black Duck generates detailed reports highlighting:
  - Vulnerable components.
  - Severity levels.
  - Recommendations for remediation (upgrades, patches).

### 5. **Remediation**
- Review the report and prioritize vulnerabilities based on severity and potential impact.
- Update or replace vulnerable components to mitigate risks.
- Implement security patches as recommended.

### 6. **Continuous Monitoring**
- Set up Black Duck for continuous monitoring to detect new vulnerabilities in real-time.
- Reg


# Question- How Spring Scheduler Works

## Overview
Spring Scheduler is part of the Spring Framework that provides a simple way to schedule tasks to be executed at specified intervals or at specific times.

## Key Components

### 1. Task Scheduling Annotations
Spring provides annotations to define scheduled tasks:
- **`@Scheduled`**: Indicates that a method should be scheduled for execution. It can take parameters to define the schedule.
  
  **Example**:
  ```java
  @Scheduled(fixedRate = 5000)
  public void performTask() {
      // Task to be executed
  }

## 2. Scheduling Configuration
To enable scheduling, you need to annotate your configuration class with @EnableScheduling.

```java
@Configuration
@EnableScheduling
public class AppConfig {
}
```

## 3. Scheduled Task Example

Here’s an example of a simple scheduled task that runs every 5 seconds.

```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class MyScheduledTask {

    @Scheduled(fixedRate = 5000)
    public void executeTask() {
        System.out.println("Task executed at: " + System.currentTimeMillis());
    }
}
```

## 4. Types of Scheduling
Fixed Rate: The task is executed at a fixed interval. If the task execution takes longer than the interval, the next execution will wait until the current task finishes.

Fixed Delay: The task is executed after a fixed delay from the completion of the last execution.

Cron Expressions: For more complex scheduling, you can use cron expressions to specify exact times and dates for task execution.

```java

@Scheduled(cron = "0 0/1 * * * ?") // Every minute
public void executeCronTask() {
    System.out.println("Cron task executed at: " + System.currentTimeMillis());
}
```

## 5. Thread Pool
By default, Spring uses a simple thread pool to manage scheduled tasks. You can customize the thread pool by defining a TaskScheduler bean.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.scheduling.concurrent.ThreadPoolTaskScheduler;

@Bean
public ThreadPoolTaskScheduler taskScheduler() {
    ThreadPoolTaskScheduler scheduler = new ThreadPoolTaskScheduler();
    scheduler.setPoolSize(5); // Set the number of threads
    return scheduler;
}
```

## Question- How to set different config for different environments

src/main/resources/
├── application.properties        # Default properties
├── application-dev.properties    # Development properties
├── application-staging.properties # Staging properties
└── application-prod.properties    # Production properties

**Setting active profile**
export SPRING_PROFILES_ACTIVE=dev

## Question - Save vs Flush in hibernate
## Save vs Flush in Hibernate

### Save
- **Purpose**: The `save()` method is used to persist an entity in the database.
- **Behavior**: It assigns a generated identifier to the entity and schedules it for insertion in the database.
- **Transaction Management**: The actual database operation occurs when the transaction is committed.
- **Return Value**: Returns the identifier of the saved entity.

### Flush
- **Purpose**: The `flush()` method is used to synchronize the Hibernate session with the database.
- **Behavior**: It forces the Hibernate Session to execute all pending SQL statements to the database.
- **Timing**: It does not commit the transaction; it only ensures that the changes made are reflected in the database.
- **Return Value**: Does not return any value.

### Key Differences
- `save()` is about persisting an entity, while `flush()` is about synchronizing the session state with the database.
- `save()` may not immediately execute any SQL, while `flush()` ensures that all pending operations are executed.


## Question- Working of @Transactional in Spring

### Overview
The `@Transactional` annotation in Spring is used to manage transactions declaratively. It ensures that a series of operations are executed in a single transaction context, providing ACID (Atomicity, Consistency, Isolation, Durability) properties.

### How It Works

1. **Annotation Placement**:
   - Can be placed at the class level or method level.
   - If placed on a class, it applies to all public methods within that class.

2. **Proxy Creation**:
   - When a bean with the `@Transactional` annotation is created, Spring creates a proxy around the bean.
   - The proxy intercepts method calls and applies transaction management logic.

3. **Transaction Management**:
   - When a method annotated with `@Transactional` is called:
     - Spring starts a new transaction or joins an existing one based on the propagation settings.
     - All database operations within the method are executed.

4. **Commit or Rollback**:
   - If the method completes successfully, the transaction is committed.
   - If an unchecked exception (runtime exception) is thrown, the transaction is rolled back.
   - Checked exceptions can be configured to trigger a rollback based on settings.

5. **Isolation Levels**:
   - The `@Transactional` annotation allows you to specify the isolation level of the transaction, which controls the visibility of changes made by other transactions.

6. **Timeout**:
   - You can define a timeout for the transaction, after which it will be rolled back if not completed.

### Example
```java
import org.springframework.transaction.annotation.Transactional;

@Service
public class UserService {

    @Transactional
    public void registerUser(User user) {
        // Perform database operations
        userRepository.save(user);
        // Other operations
    }
}
```

## Question- Different Caches in Hibernate

Hibernate provides a caching mechanism to enhance performance by reducing database access. There are two main levels of caching in Hibernate:

### 1. First-Level Cache (Session Cache)
- **Scope**: It is associated with the `Session` object.
- **Lifetime**: It lasts until the session is closed.
- **Usage**: Whenever you load an entity, Hibernate checks the first-level cache. If the entity is already present in the cache, it retrieves it from there instead of querying the database.
- **Eviction**: The first-level cache is automatically cleared when the session is closed.

### 2. Second-Level Cache
- **Scope**: It is associated with the `SessionFactory` and can be shared across multiple sessions.
- **Lifetime**: It lasts as long as the `SessionFactory` is open.
- **Configuration**: Must be explicitly enabled in the Hibernate configuration.
- **Providers**: Supports various cache providers (e.g., EHCache, Infinispan, Hazelcast, etc.).
- **Usage**: Useful for caching entities, collections, and queries, reducing database calls for frequently accessed data.

### 3. Query Cache
- **Scope**: This is an optional cache that caches the results of specific queries.
- **Usage**: When enabled, Hibernate caches the results of a query and uses it for subsequent executions if the underlying data has not changed.
- **Dependencies**: The query cache relies on the second-level cache and must be enabled for it to work.

### Key Points
- **Caching Strategy**: You can define caching strategies (e.g., read-only, read-write, nonstrict-read-write, etc.) for entities and collections to optimize performance.
- **Configuration**: Caching settings can be specified in the Hibernate configuration files or annotations on entity classes.

### Example
To enable the second-level cache with annotations:
```java
@Entity
@Cacheable
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class Product {
    // ...
}
```


### Question- Writing native queries in JPA

## Writing Native Queries in JPA

In Java Persistence API (JPA), native queries are SQL queries that are executed directly against the database. They provide a way to perform operations that are not possible using JPQL (Java Persistence Query Language) or Criteria API. Here's how to write and use native queries in JPA.

### 1. Using `@Query` Annotation

You can use the `@Query` annotation in your repository interface to define a native query. 

#### Example:

```java
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProductRepository extends CrudRepository<Product, Long> {

    @Query(value = "SELECT * FROM products WHERE price > ?1", nativeQuery = true)
    List<Product> findProductsAbovePrice(double price);
}
```

## 2. Using EntityManager
You can also execute native queries using the EntityManager interface.

```java
import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.persistence.Query;
import java.util.List;

public class ProductService {

    @PersistenceContext
    private EntityManager entityManager;

    public List<Product> getProductsAbovePrice(double price) {
        String sql = "SELECT * FROM products WHERE price > :price";
        Query query = entityManager.createNativeQuery(sql, Product.class);
        query.setParameter("price", price);
        return query.getResultList();
    }
}
```
## 3. Named Native Queries
You can define named native queries in your entity class using the @NamedNativeQuery annotation.

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.NamedNativeQuery;

@Entity
@NamedNativeQuery(
    name = "Product.findAbovePrice",
    query = "SELECT * FROM products WHERE price > :price",
    resultClass = Product.class
)
public class Product {
    @Id
    private Long id;
    private String name;
    private double price;

    // Getters and Setters
}

//Can use the named queries like this in repository

import org.springframework.stereotype.Repository;
import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.persistence.Query;
import java.util.List;

@Repository
public class ProductRepository {

    @PersistenceContext
    private EntityManager entityManager;

    public List<Product> findProductsAbovePrice(double price) {
        Query query = entityManager.createNamedQuery("Product.findAbovePrice");
        query.setParameter("price", price);
        return query.getResultList();
    }
}

```

## Question- How to implement pagination in JPA

## Pagination in JPA

Pagination in Java Persistence API (JPA) allows you to retrieve large datasets in smaller, manageable chunks. This is especially useful for improving performance and user experience when dealing with large amounts of data. Here’s how pagination works in JPA:

### 1. Using the `Pageable` Interface

Spring Data JPA provides a `Pageable` interface, which helps manage pagination details like the page number, size, and sorting.

#### Example:

```java
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    Page<Product> findAll(Pageable pageable);
}
```

### 2. Using PageRequest
You can create a PageRequest object to specify the page number and size.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.stereotype.Service;

@Service
public class ProductService {

    @Autowired
    private ProductRepository productRepository;

    public Page<Product> getProducts(int page, int size) {
        PageRequest pageRequest = PageRequest.of(page, size);
        return productRepository.findAll(pageRequest);
    }
}


//Then accessing results like this
/*getContent(): Returns the content of the current page.
getTotalPages(): Returns the total number of pages.
getTotalElements(): Returns the total number of elements across all pages.
hasNext(): Checks if there is a next page.
hasPrevious(): Checks if there is a previous page.
*/

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class ProductController {

    @Autowired
    private ProductService productService;

    @GetMapping("/products")
    public Page<Product> getProducts(@RequestParam int page, @RequestParam int size) {
        return productService.getProducts(page, size);
    }
}

```


### 3. Custom Queries with Pagination
You can also use pagination with custom queries defined using the @Query annotation.

```java
import org.springframework.data.domain.Pageable;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.PagingAndSortingRepository;

public interface CustomProductRepository extends PagingAndSortingRepository<Product, Long> {

    @Query("SELECT p FROM Product p WHERE p.price > ?1")
    Page<Product> findByPriceGreaterThan(double price, Pageable pageable);
}

```


## Question-  Embedding Composite Keys in Entity

A composite key is a combination of multiple columns that uniquely identify a row in a database table. When you want to use a composite key as the primary key for an entity in your application, you need to ensure that the entity correctly represents and manages this composite key.

### Steps to Embed Composite Keys:

1. **Define the Composite Key Columns:**
   - Identify the columns that together form the composite key. These columns should be non-nullable and unique for each row.
   - Define corresponding properties in your entity class, using appropriate data types.

2. **Create a Composite Key Class:**
   - If the composite key is complex or frequently used, consider creating a separate class to represent it. This can improve code readability and maintainability.
   - The composite key class should contain properties for each column of the composite key.

3. **Annotate the Composite Key:**
   - Use the appropriate annotation provided by your ORM framework to mark the composite key class or properties as a composite key.
   - For example, in JPA, you would use the `@Embeddable` annotation for the composite key class and the `@EmbeddedId` annotation for the property referencing the composite key.

4. **Set the Composite Key as the Primary Key:**
   - Annotate the property or field in your entity class that references the composite key with the appropriate annotation to indicate that it is the primary key.
   - For example, in JPA, you would use the `@Id` annotation.

### Example (JPA):

```java
@Embeddable
public class CompositeKey {
    @Column(name = "column1")
    private String column1;

    @Column(name = "column2")
    private int column2;

    // Getters and setters
}

@Entity
public class MyEntity {
    @EmbeddedId
    private CompositeKey id;

    // Other properties
}

```

## Question- How to handle fault tolerance in microservices
## How to Handle Fault Tolerance in Microservices

Fault tolerance in microservices is crucial to maintain the availability and reliability of distributed systems. Various strategies and tools can be used to handle failures effectively. Below are some common patterns and methods to ensure fault tolerance in microservices architecture:

### 1. **Circuit Breaker Pattern**
The **Circuit Breaker Pattern** prevents cascading failures in a microservices architecture by stopping attempts to invoke a failing service after a certain threshold of failures is reached.

- **Closed State**: Requests are sent normally to the service.
- **Open State**: If the service fails repeatedly, the circuit opens, and no more requests are sent until the service is healthy.
- **Half-Open State**: After a cooldown period, a limited number of requests are allowed to see if the service has recovered.

#### Example Using Resilience4j (Spring Boot):
```java
import io.github.resilience4j.circuitbreaker.annotation.CircuitBreaker;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class FaultTolerantService {

    @GetMapping("/getData")
    @CircuitBreaker(name = "myService", fallbackMethod = "fallback")
    public String getData() {
        // Call to another microservice
    }

    public String fallback(Throwable t) {
        return "Fallback response";
    }
}
```

## 2. Retry Pattern
In cases of transient failures, the Retry Pattern automatically retries the failed request a specified number of times before giving up. This is useful when failures may resolve themselves after a short period.

```java
import org.springframework.retry.annotation.Retryable;
import org.springframework.stereotype.Service;

@Service
public class RetryService {

    @Retryable(maxAttempts = 3)
    public String fetchData() {
        // Logic to fetch data, retry in case of failure
    }
}

```

## 3. Timeouts
Implementing timeouts prevents the application from waiting indefinitely for a response from a failing service. By setting a timeout, the application can move on to another task or fail gracefully.

Example Using Feign Client:

feign:
  client:
    config:
      default:
        connectTimeout: 5000
        readTimeout: 5000
        
## 4. Bulkhead Pattern
The Bulkhead Pattern isolates different parts of the system so that failures in one microservice do not cause failures in others. It is analogous to partitioning a ship into separate sections so that flooding in one section doesn’t sink the entire ship.

Allocate separate thread pools or resource quotas for different services.
Example:
Service A and Service B are allocated separate thread pools to avoid resource exhaustion when Service A fails.

## 5. Fallback Pattern
The Fallback Pattern provides an alternative response when a service is down. This can be a default value, a cached response, or a graceful degradation of service.

Example Using Resilience4j:
```java
@CircuitBreaker(name = "myService", fallbackMethod = "fallback")
public String getData() {
    // Call to another microservice
}

public String fallback(Throwable t) {
    return "Default Fallback Data";
}
```

## 6. Health Monitoring and Alerts
Implementing health checks for microservices and setting up monitoring tools (like Prometheus, Grafana) can help detect and react to failures in real-time.

Health Check Endpoints: Expose /health or /actuator/health endpoints for monitoring service status.
Alerting: Trigger alerts when failures or latency increases occur.

## 7. Service Mesh
Using service meshes (like Istio or Linkerd) adds an additional layer for managing microservices communication, load balancing, and fault tolerance. It abstracts away much of the retry, timeout, and circuit breaker logic from the application.




## Question- Transaction management in microservices
## Transaction Management in Microservices

In microservices architecture, managing transactions across services can be challenging due to their distributed nature. Traditional ACID transactions (Atomicity, Consistency, Isolation, Durability) are difficult to achieve across multiple services. To handle transactions in microservices, alternative approaches are used to ensure **eventual consistency** while maintaining reliability.

### 1. **Two-Phase Commit (2PC)**
The **Two-Phase Commit (2PC)** protocol is a distributed algorithm that coordinates a global transaction across multiple services.

- **Phase 1 (Prepare)**: The coordinator asks each service (participant) to prepare for the transaction.
- **Phase 2 (Commit/Rollback)**: If all participants are prepared, the coordinator sends a commit message. If any participant fails, a rollback is triggered.

While 2PC ensures atomicity, it is rarely used in microservices due to its **performance bottlenecks** and the risk of **blocking resources** during the commit phase.

### 2. **Saga Pattern**
The **Saga Pattern** is a widely-used approach for managing transactions in microservices by breaking a long-running transaction into smaller, local transactions.

- Each service involved in the transaction performs a local commit.
- If one transaction fails, compensating transactions are executed to undo the preceding operations.

#### Types of Saga Patterns:
- **Choreography**: Each service reacts to events and triggers the next action.
- **Orchestration**: A central orchestrator service manages the flow of transactions and sends commands to other services.

#### Example of Choreography-Based Saga:
```java
// Example: Order service creates an order
public void createOrder() {
    // Local transaction
    orderRepository.save(order);

    // Publish an event to trigger other services
    eventPublisher.publish(new OrderCreatedEvent(order));
}
```

## 3. Eventual Consistency
In a distributed system, eventual consistency ensures that, while not immediately consistent, the system will become consistent over time. This is achieved by:

Event-Driven Architecture: Services communicate through events, allowing them to operate asynchronously and independently. Failures are handled by retry mechanisms and error handling.
Message Queues: Systems like Kafka or RabbitMQ can be used to decouple services and ensure reliable delivery of events, supporting eventual consistency.

## 4. Outbox Pattern
The Outbox Pattern ensures reliable event publishing along with local transactions. A service first writes both the event and the state change to the same local database. A separate service or mechanism then reads the event from the outbox and publishes it to other services.

Example Flow:
Step 1: Write the transaction data and event into the local database.
Step 2: A polling process reads the outbox table and publishes the event.

## 5. Compensating Transactions
In case of failure, compensating transactions are executed to undo the effects of previous transactions, ensuring the system reaches a consistent state. This is a crucial aspect of the Saga Pattern and is essential in a microservices environment where distributed transactions can't be rolled back easily.

## 6. Distributed Transactions with Spring Boot
In Spring-based microservices, distributed transactions are managed by external frameworks such as Atomikos or Narayana, but most often, microservices adopt Saga or event-driven approaches due to their scalability.

Example Saga Orchestration with Spring:
```java
@Service
public class OrderSagaOrchestrator {

    @Autowired
    private PaymentService paymentService;

    @Transactional
    public void placeOrder(Order order) {
        // Local transaction
        orderRepository.save(order);

        // Call other microservices in sequence
        paymentService.processPayment(order);
        shippingService.shipOrder(order);
    }
}

```


## Question- Global exception Springboot
## Global Exception Handling in Spring Boot

In Spring Boot, global exception handling can be managed using the `@ControllerAdvice` annotation, which allows you to handle exceptions across the entire application in one global location.

### Example of Global Exception Handling

Here’s an example of how to implement global exception handling in a Spring Boot application:

```java
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.context.request.WebRequest;

@ControllerAdvice
public class GlobalExceptionHandler {

    // Handle specific exception
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<?> handleResourceNotFoundException(ResourceNotFoundException ex, WebRequest request) {
        ErrorDetails errorDetails = new ErrorDetails(ex.getMessage(), request.getDescription(false));
        return new ResponseEntity<>(errorDetails, HttpStatus.NOT_FOUND);
    }

    // Handle generic exceptions
    @ExceptionHandler(Exception.class)
    public ResponseEntity<?> handleGlobalException(Exception ex, WebRequest request) {
        ErrorDetails errorDetails = new ErrorDetails("Internal Server Error", request.getDescription(false));
        return new ResponseEntity<>(errorDetails, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}


public class ErrorDetails {

    private String message;
    private String details;

    public ErrorDetails(String message, String details) {
        this.message = message;
        this.details = details;
    }

    // Getters and setters
    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public String getDetails() {
        return details;
    }

    public void setDetails(String details) {
        this.details = details;
    }
}


public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}



```



## Question- JPA vs SpringData vs Hibernate

## JPA, Spring Data, and Hibernate

### 1. **JPA (Java Persistence API)**:
- **Definition**: JPA is a specification provided by Java for managing relational data in applications using Java objects. It defines a set of rules and guidelines for Object-Relational Mapping (ORM).
- **Purpose**: JPA allows you to map Java classes to database tables and perform CRUD operations. It is not a framework but an abstraction that ORM tools like Hibernate can implement.
- **Key Features**:
  - Annotations such as `@Entity`, `@Id`, `@Table`, etc., are used to map Java objects to relational tables.
  - Supports JPQL (Java Persistence Query Language) for querying databases.
  - Does not provide actual implementation; it needs a provider like Hibernate to work.

### 2. **Spring Data JPA**:
- **Definition**: Spring Data JPA is a part of the larger Spring Data project. It simplifies data access by providing a higher-level abstraction over JPA.
- **Purpose**: It eliminates the need for boilerplate code by using repository patterns, making database access operations more manageable.
- **Key Features**:
  - Provides `CrudRepository` and `JpaRepository` interfaces for CRUD operations.
  - Auto-generates queries based on method names using conventions like `findByName`, `deleteById`, etc.
  - Allows for the customization of queries using JPQL, SQL, and even the Criteria API.
  
```java
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    List<Employee> findByLastName(String lastName);
}
```

## 3. Hibernate:
Definition: Hibernate is a widely-used ORM framework that implements JPA. It is a full-fledged framework for managing database operations with Java objects.
Purpose: Hibernate allows for advanced ORM functionalities and provides additional features over JPA. It supports a wide range of databases and simplifies complex data management tasks.
Key Features:
Lazy/Eager fetching strategies to load data on-demand.
Caching mechanisms for optimizing database access (First-Level Cache, Second-Level Cache).
Supports complex queries, joins, and mapping configurations.
Provides session management and transaction handling.


Relationship:
JPA: Defines the standard for ORM.
Hibernate: A framework that implements the JPA specification and adds additional features.
Spring Data JPA: Provides a simplified and higher abstraction over JPA, reducing the need for boilerplate code in a Spring-based application.

```java
## Example of Code Using JPA with Hibernate

Here’s a basic example of how you can use JPA with Hibernate in a Spring Boot project to interact with a database.

### 1. **Entity Class**

The entity class represents a table in the database.

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String firstName;
    private String lastName;
    private String email;

    // Constructors, getters, and setters
    public Employee() {}

    public Employee(String firstName, String lastName, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
    }

    // Getters and Setters
}


import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    // Custom query methods if needed
    List<Employee> findByLastName(String lastName);
}


import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    // Custom query methods if needed
    List<Employee> findByLastName(String lastName);
}

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    @GetMapping
    public List<Employee> getAllEmployees() {
        return employeeService.getAllEmployees();
    }

    @GetMapping("/{id}")
    public Employee getEmployeeById(@PathVariable Long id) {
        return employeeService.getEmployeeById(id);
    }

    @PostMapping
    public Employee createEmployee(@RequestBody Employee employee) {
        return employeeService.saveEmployee(employee);
    }

    @DeleteMapping("/{id}")
    public void deleteEmployee(@PathVariable Long id) {
        employeeService.deleteEmployee(id);
    }
}

spring.datasource.url=jdbc:mysql://localhost:3306/employeedb
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

```

**A**
# A
## A
### A
