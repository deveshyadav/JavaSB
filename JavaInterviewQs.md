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

### 3. Hibernate:
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


## Question -Features of java 17

Java 17, released as a Long-Term Support (LTS) version, brought several improvements and new features to the language. Here are some key highlights:

### 1. **Sealed Classes (JEP 409)**
Sealed classes allow you to restrict which other classes or interfaces may extend or implement them. This feature helps in controlling the inheritance hierarchy.

```java
public abstract sealed class Shape permits Circle, Rectangle { }
public final class Circle extends Shape { }
public final class Rectangle extends Shape { }
```
### 2. Pattern Matching for switch (Preview) (JEP 406)
Pattern matching in switch statements simplifies how you handle conditional logic based on the type of an object. This feature was introduced as a preview in Java 17.
```java
switch (shape) {
    case Circle c -> System.out.println("Circle with radius " + c.radius());
    case Rectangle r -> System.out.println("Rectangle with area " + r.area());
    default -> throw new IllegalArgumentException("Unknown shape");
}

```

### 3. Strong Encapsulation by Default (JEP 403)
With Java 17, the encapsulation of the JDK internals becomes stronger by default. This means that access to internal APIs (like sun.misc.Unsafe) is further restricted unless explicitly allowed via command-line flags.

### 4. Context-Specific Deserialization Filters (JEP 415)
This feature provides a mechanism to improve security by allowing applications to configure deserialization filters for incoming streams. It helps in preventing attacks like deserialization vulnerabilities.

### 5. Removal of the Applet API (JEP 398)
The Applet API, which has been considered outdated, was finally removed in Java 17. Applets were already deprecated and rarely used due to modern web alternatives like HTML5.

### 6. Foreign Function & Memory API (Incubator) (JEP 412)
Introduced as an incubator feature, this API allows Java programs to interact with native code and access foreign memory outside the Java heap in a more efficient way.

### 7. Vector API (Second Incubator) (JEP 414)
The second incubation of the Vector API allows developers to express vector computations, which can be optimized at runtime for better performance on supported hardware architectures.

### 8. Deprecate the Security Manager for Removal (JEP 411)
Java 17 deprecates the Security Manager with the intention of removing it in a future release. This was historically used for sandboxing applications, but it has become less relevant with modern security practices.

### 9. macOS/AArch64 Port (JEP 391)
This feature adds support for the macOS/AArch64 platform, which is particularly useful with the growing popularity of Apple Silicon (M1 chip).

### 10. Text Blocks (Standardized)
Though introduced in earlier versions, text blocks are now fully supported in Java 17. They allow multi-line strings that simplify code readability, especially for JSON, XML, and SQL queries.

```java
String json = """
              {
                  "name": "John",
                  "age": 30
              }
              """;
```
### 11. Garbage Collection Improvements
Java 17 includes improvements to the Z Garbage Collector (ZGC) and the G1 Garbage Collector, making them more efficient in memory management and reducing application pause times.

### 12. Deprecation of RMI Activation (JEP 407)
The Remote Method Invocation (RMI) Activation mechanism has been deprecated, which was rarely used in modern applications.



## Question- MongoDB vs Mysql
## MongoDB vs MySQL

### 1. **Data Model**
- **MongoDB**: NoSQL, document-based database that stores data in flexible, JSON-like BSON (Binary JSON) documents. It is schema-less, meaning the structure of the data can vary across documents in the same collection.
- **MySQL**: Relational database management system (RDBMS) that stores data in tables with fixed schemas. It uses SQL (Structured Query Language) to manage and query data.

### 2. **Schema**
- **MongoDB**: Schema-less, allowing dynamic and flexible document structures. This is useful for applications where data structures change frequently.
- **MySQL**: Schema-based, requiring a predefined structure with tables, rows, and columns. Data must adhere to the specified schema.

### 3. **Scalability**
- **MongoDB**: Horizontal scaling (sharding) is built-in and is suitable for large-scale applications. It scales out by distributing data across multiple servers.
- **MySQL**: Typically scales vertically (by upgrading hardware). Horizontal scaling (sharding) is possible but more complex to implement compared to MongoDB.

### 4. **Transactions**
- **MongoDB**: Supports multi-document ACID transactions (starting from version 4.0), but transactions are typically more lightweight and limited compared to relational databases.
- **MySQL**: Strong support for ACID transactions, making it ideal for applications requiring high data integrity (e.g., banking systems).

### 5. **Query Language**
- **MongoDB**: Uses a flexible query language that is JSON-like. It supports complex queries with aggregation pipelines.
- **MySQL**: Uses SQL, a standard and widely adopted query language with powerful features for joining, filtering, grouping, and manipulating data.

### 6. **Performance**
- **MongoDB**: Excels with large datasets, read-heavy workloads, and unstructured data. Its performance is better for applications that don't require complex joins.
- **MySQL**: Performs well with structured data and when executing complex joins. However, it may struggle with very large datasets unless optimized.

### 7. **Use Cases**
- **MongoDB**: Best suited for applications with unstructured or semi-structured data, such as content management systems, real-time analytics, and IoT applications.
- **MySQL**: Ideal for applications that require structured data and ACID compliance, such as financial systems, e-commerce platforms, and enterprise resource planning (ERP) systems.

### 8. **Indexes**
- **MongoDB**: Supports a variety of index types (e.g., single field, compound, geospatial). Indexes are stored as BSON objects and can handle large, distributed datasets.
- **MySQL**: Uses B-tree indexes for optimal performance on primary keys, foreign keys, and commonly queried columns. Indexing plays a major role in performance optimization for complex queries.

### 9. **Joins**
- **MongoDB**: Does not support traditional SQL-style joins. Instead, it relies on embedding or linking documents through references. Aggregation pipelines can be used for similar functionality.
- **MySQL**: Supports complex joins between multiple tables, which makes it ideal for relational data with multiple associations.

### 10. **Backup and Recovery**
- **MongoDB**: Offers point-in-time backups, but its distributed nature makes recovery slightly more complex.
- **MySQL**: Provides built-in support for backups (using tools like `mysqldump`), and recovery processes are well-established and simpler for single-node setups.

### 11. **Community & Support**
- **MongoDB**: Growing rapidly with a large community of developers, particularly in the NoSQL and big data space.
- **MySQL**: One of the most popular databases worldwide, with a vast community and a large array of online resources.

### **Summary of Key Differences:**
- **MongoDB**: Flexible, schema-less, NoSQL database ideal for large, unstructured, or semi-structured datasets.
- **MySQL**: Structured, schema-based RDBMS that excels at handling relational data with powerful SQL queries.


## Question- Spriongboot key components
## Spring Boot Key Components

### 1. **Spring Boot Starter**
- **Description**: Starters are a set of convenient dependency descriptors you can include in your application. They simplify Maven or Gradle configuration by grouping common dependencies for various functionalities.
- **Example**: `spring-boot-starter-web` includes dependencies for building web applications, including Spring MVC, Tomcat, and Jackson.

### 2. **Spring Boot Auto-Configuration**
- **Description**: This feature automatically configures your Spring application based on the dependencies present on the classpath. It reduces the need for manual bean configuration.
- **How it Works**: It uses the `@EnableAutoConfiguration` annotation to enable auto-configuration and relies on conditional configurations to determine which beans to create.

### 3. **Spring Boot Actuator**
- **Description**: Provides built-in endpoints for monitoring and managing Spring Boot applications in production. It exposes operational information about the application.
- **Features**: Health checks, metrics gathering, environment details, and more can be accessed via HTTP endpoints or JMX.

### 4. **Spring Boot CLI**
- **Description**: A command-line tool that allows you to run and test Spring Boot applications quickly without the need for a full development environment.
- **Usage**: You can create Groovy scripts and run them using the CLI to quickly prototype or build applications.

### 5. **Spring Boot Initializr**
- **Description**: A web-based tool (https://start.spring.io/) that allows you to quickly generate a Spring Boot project with your desired dependencies and configurations.
- **Usage**: You can select project metadata (like Group, Artifact, Name) and dependencies, and it generates a ZIP file containing the project structure.

### 6. **Spring Boot Configuration Properties**
- **Description**: Allows externalizing configuration properties in application.properties or application.yml files. You can bind these properties to Java objects using `@ConfigurationProperties`.
- **Example**:
  ```java
  @ConfigurationProperties(prefix = "app")
  public class AppConfig {
      private String name;
      private String version;
      // getters and setters
  }
  ```


### 7. Embedded Servers
- **Description**: Spring Boot supports embedded servers like Tomcat, Jetty, and Undertow, allowing you to run applications without deploying them to an external server.
- **Benefit**: Simplifies the deployment process by packaging the server within the application itself.

### 8. Spring Boot Testing
- **Description**: Provides utilities and annotations to facilitate testing Spring Boot applications. It includes support for unit tests, integration tests, and mocking.
- **Annotations**: Commonly used annotations include `@SpringBootTest`, `@MockBean`, and `@DataJpaTest`.

### 9. Spring Boot Profiles
- **Description**: Profiles allow you to create different configurations for different environments (e.g., dev, test, prod). You can activate a profile using the `spring.profiles.active` property.
- **Usage**: You can define environment-specific properties in files like `application-dev.properties` and `application-prod.properties`.

### 10. Spring Boot DevTools
- **Description**: A set of tools that enhance the development experience by providing features like automatic restarts, live reload, and enhanced error messages.
- **Usage**: It speeds up development cycles by reducing the need for manual restarts.


## Question- ImportNT Linux commands

# Important Linux Commands

1. **ls**: List files and directories.
2. **cd**: Change directory.
3. **pwd**: Print working directory.
4. **mkdir**: Create a new directory.
5. **rmdir**: Remove an empty directory.
6. **rm**: Remove files or directories.
7. **cp**: Copy files or directories.
8. **mv**: Move or rename files or directories.
9. **cat**: View contents of a file.
10. **less**: View file content page by page.
11. **echo**: Display a line of text or a variable value.
12. **chmod**: Change file permissions.
13. **chown**: Change file owner and group.
14. **ps**: Display currently running processes.
15. **top**: Show real-time system resource usage.


## Question- Controller vs RestController
# @Controller vs @RestController

## @Controller
- **Purpose**: Indicates that a class serves as a controller in the Spring MVC framework.
- **Response Type**: Returns a view name (JSP, HTML) that is resolved by a view resolver.
- **Usage**: Typically used in web applications where server-side rendering is needed.

## @RestController
- **Purpose**: Combines `@Controller` and `@ResponseBody`, indicating that the class serves RESTful web services.
- **Response Type**: Returns JSON or XML responses directly from the methods, without needing a view resolver.
- **Usage**: Ideal for building REST APIs where data is exchanged in formats like JSON.



## Question- Important HTTP codes
# Important HTTP Status Codes

1. **200 OK**
   - **Usage**: Request succeeded, and the server returned the requested data.

2. **201 Created**
   - **Usage**: Resource successfully created, often used in response to POST requests.

3. **204 No Content**
   - **Usage**: Request succeeded, but there's no content to send back (often used for DELETE requests).

4. **301 Moved Permanently**
   - **Usage**: The requested resource has been permanently moved to a new URL.

5. **302 Found**
   - **Usage**: The requested resource temporarily resides under a different URI.

6. **400 Bad Request**
   - **Usage**: The server cannot process the request due to a client error (e.g., malformed request syntax).

7. **401 Unauthorized**
   - **Usage**: Authentication is required and has failed or has not yet been provided.

8. **403 Forbidden**
   - **Usage**: The server understands the request but refuses to authorize it.

9. **404 Not Found**
   - **Usage**: The requested resource could not be found on the server.

10. **500 Internal Server Error**
    - **Usage**: A generic error message indicating that the server encountered an unexpected condition.

11. **502 Bad Gateway**
    - **Usage**: The server, while acting as a gateway, received an invalid response from an upstream server.

12. **503 Service Unavailable**
    - **Usage**: The server is currently unable to handle the request due to temporary overloading or maintenance.



## Question- What is docker? What problem it solved, and benefits.
# What is Docker?

Docker is an open-source platform that automates the deployment, scaling, and management of applications within lightweight, portable containers. A container packages an application and its dependencies into a single executable unit, ensuring consistency across different environments.

## Problems Solved by Docker

1. **Environment Consistency**:
   - Docker eliminates the "it works on my machine" problem by ensuring that applications run the same way across development, testing, and production environments.

2. **Dependency Management**:
   - It allows developers to package all the dependencies required for an application within the container, simplifying the setup process.

3. **Isolation**:
   - Each container runs in its own environment, providing process isolation and improving security.

4. **Resource Efficiency**:
   - Containers share the host OS kernel, making them lightweight and quick to start compared to traditional virtual machines.

5. **Scalability**:
   - Docker makes it easy to scale applications by creating multiple instances of containers quickly.

## Benefits of Docker

1. **Portability**:
   - Applications packaged in Docker containers can run on any machine that has Docker installed, regardless of the underlying OS.

2. **Speed**:
   - Containers can be started almost instantly, leading to faster deployment cycles.

3. **Version Control**:
   - Docker images can be versioned, allowing teams to track changes and roll back to previous versions easily.

4. **Microservices Architecture**:
   - Docker supports microservices by allowing each service to run in its own container, making it easier to develop, deploy, and manage.

5. **Community and Ecosystem**:
   - Docker has a vast community and rich ecosystem, including Docker Hub, which provides a repository for sharing container images.

6. **CI/CD Integration**:
   - Docker integrates well with continuous integration and continuous deployment (CI/CD) tools, streamlining the development workflow.


## Question- SOLID priniciples

# SOLID Principles

SOLID is an acronym that represents five design principles intended to make software designs more understandable, flexible, and maintainable. These principles are especially relevant in object-oriented programming and are aimed at improving software design. 

## 1. Single Responsibility Principle (SRP)
- **Definition**: A class should have only one reason to change, meaning it should have only one job or responsibility.
- **Benefit**: Reduces the complexity of the class and makes it easier to understand and maintain. Changes to one part of the functionality will not affect other parts.

## 2. Open/Closed Principle (OCP)
- **Definition**: Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
- **Benefit**: This principle encourages the use of interfaces or abstract classes, allowing new functionality to be added without changing existing code. It promotes code stability and reduces the risk of introducing bugs.

## 3. Liskov Substitution Principle (LSP)
- **Definition**: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
- **Benefit**: Ensures that a subclass can stand in for its superclass, promoting the use of polymorphism and enhancing code reusability.

## 4. Interface Segregation Principle (ISP)
- **Definition**: No client should be forced to depend on methods it does not use. Interfaces should be specific to a client’s needs.
- **Benefit**: Reduces the impact of changes and minimizes the number of dependencies in the code. Clients will only need to know about the methods that are relevant to them, leading to more focused and cohesive interfaces.

## 5. Dependency Inversion Principle (DIP)
- **Definition**: High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces). Abstractions should not depend on details; details should depend on abstractions.
- **Benefit**: This principle promotes loose coupling and enhances code flexibility and testability by decoupling the high-level business logic from low-level implementation details.

## Summary
Adhering to the SOLID principles leads to a more robust and maintainable codebase, facilitating easier updates, modifications, and collaboration among developers. These principles can guide software design decisions, ultimately improving the quality of the software system.


## Question- Details of all collections

# Java Collections Overview

Java Collections Framework provides various data structures to store, manipulate, and retrieve data. Here’s a detailed breakdown of the key properties, features, initial capacity, and load factor of the main collection types in Java.

## 1. **List**
### Properties:
- **Ordered**: Maintains the order of insertion.
- **Allows Duplicates**: Can store duplicate elements.
  
### Features:
- Dynamic resizing of the underlying array.
- Can be accessed via indices, allowing random access.
  
### Common Implementations:

#### a. **ArrayList**
- **Description**: Resizable array implementation of the List interface.
- **Initial Capacity**: 10 (default).
- **Load Factor**: Not applicable (resizes when the size exceeds the current capacity).
- **Usage**: Suitable for storing a list of elements where frequent access by index is required.
- **Performance**:
  - **Get**: O(1)
  - **Add**: O(1) (amortized)
  - **Remove**: O(n)

#### b. **LinkedList**
- **Description**: Doubly-linked list implementation of the List interface.
- **Initial Capacity**: Not defined; grows as needed.
- **Load Factor**: Not applicable.
- **Usage**: Suitable for applications where frequent insertion and deletion operations occur.
- **Performance**:
  - **Get**: O(n)
  - **Add**: O(1)
  - **Remove**: O(1)

## 2. **Set**
### Properties:
- **Unordered**: Does not maintain any order.
- **No Duplicates**: Cannot store duplicate elements.
  
### Features:
- Uses hashing or tree structure for storage.
  
### Common Implementations:

#### a. **HashSet**
- **Description**: Hash table implementation of the Set interface.
- **Initial Capacity**: 16 (default).
- **Load Factor**: 0.75 (default).
- **Usage**: Suitable for storing unique elements with no particular order.
- **Performance**:
  - **Add**: O(1) (amortized)
  - **Contains**: O(1)
  - **Remove**: O(1)

#### b. **LinkedHashSet**
- **Description**: Hash table with a linked list maintaining insertion order.
- **Initial Capacity**: 16 (default).
- **Load Factor**: 0.75 (default).
- **Usage**: Suitable for storing unique elements while maintaining the order of insertion.
- **Performance**:
  - **Add**: O(1)
  - **Contains**: O(1)
  - **Remove**: O(1)

#### c. **TreeSet**
- **Description**: Navigable set implementation based on a Red-Black tree.
- **Initial Capacity**: 10 (default).
- **Load Factor**: Not applicable (does not use load factor).
- **Usage**: Suitable for storing unique elements in sorted order.
- **Performance**:
  - **Add**: O(log n)
  - **Contains**: O(log n)
  - **Remove**: O(log n)

## 3. **Queue**
### Properties:
- **Ordered**: Maintains the order of insertion.
- **Allows Duplicates**: Can store duplicate elements.
  
### Features:
- Follows FIFO (First In First Out) principle.
  
### Common Implementations:

#### a. **LinkedList** (Also implements Queue)
- **Description**: Doubly-linked list implementation of the Queue interface.
- **Initial Capacity**: Not defined; grows as needed.
- **Load Factor**: Not applicable.
- **Usage**: Suitable for queue operations where insertion and deletion occur at both ends.
- **Performance**:
  - **Offer**: O(1)
  - **Poll**: O(1)
  - **Peek**: O(1)

#### b. **PriorityQueue**
- **Description**: Queue implementation where elements are ordered according to their natural ordering or by a specified comparator.
- **Initial Capacity**: 11 (default).
- **Load Factor**: Not applicable (uses a heap structure).
- **Usage**: Suitable for scenarios where elements need to be processed based on priority rather than order of insertion.
- **Performance**:
  - **Add**: O(log n)
  - **Remove**: O(log n)
  - **Peek**: O(1)

## 4. **Map**
### Properties:
- **Key-Value Pairs**: Stores data as key-value pairs.
- **No Duplicate Keys**: Cannot have duplicate keys.
  
### Features:
- Keys are unique, values can be duplicated.
  
### Common Implementations:

#### a. **HashMap**
- **Description**: Hash table implementation of the Map interface.
- **Initial Capacity**: 16 (default).
- **Load Factor**: 0.75 (default).
- **Usage**: Suitable for fast key-value lookups.
- **Performance**:
  - **Put**: O(1) (amortized)
  - **Get**: O(1)
  - **Remove**: O(1)

#### b. **LinkedHashMap**
- **Description**: Hash table with a linked list maintaining insertion order.
- **Initial Capacity**: 16 (default).
- **Load Factor**: 0.75 (default).
- **Usage**: Suitable for fast key-value lookups while maintaining insertion order.
- **Performance**:
  - **Put**: O(1)
  - **Get**: O(1)
  - **Remove**: O(1)

#### c. **TreeMap**
- **Description**: Navigable map implementation based on a Red-Black tree.
- **Initial Capacity**: 10 (default).
- **Load Factor**: Not applicable (does not use load factor).
- **Usage**: Suitable for storing key-value pairs in sorted order by keys.
- **Performance**:
  - **Put**: O(log n)
  - **Get**: O(log n)
  - **Remove**: O(log n)

#### d. **Hashtable**
- **Description**: Legacy class for hash table implementation of the Map interface; synchronized.
- **Initial Capacity**: 11 (default).
- **Load Factor**: 0.75 (default).
- **Usage**: Suitable for thread-safe operations but is generally slower than HashMap.
- **Performance**:
  - **Put**: O(1)
  - **Get**: O(1)
  - **Remove**: O(1)

## Summary
Each collection type has its own unique properties, features, initial capacity, and load factor, making them suitable for various use cases. Understanding these characteristics helps in selecting the right collection for a specific scenario.


## Question- CRUD vs JPA repository
# Difference between CRUD and JPA Repository

## CRUD Operations
- **Definition**: CRUD stands for Create, Read, Update, and Delete, which are the four basic operations for managing data in a database.
- **Usage**: CRUD operations can be performed using SQL queries directly or through various frameworks and libraries that simplify data manipulation.
- **Implementation**:
  - Typically involves writing manual SQL queries or using ORM frameworks.
  - Not tied to a specific framework; can be implemented in any programming language.

## JPA Repository
- **Definition**: JPA (Java Persistence API) Repository is a part of the Spring Data framework that provides an abstraction layer for performing CRUD operations on entities in a database.
- **Usage**: JPA repositories offer built-in methods for common CRUD operations without the need for writing boilerplate code.
- **Implementation**:
  - Extends `JpaRepository` or `CrudRepository` interface provided by Spring Data JPA.
  - Automatically generates SQL queries based on method names, reducing the need for manual query writing.

## Key Differences
| Feature                 | CRUD                                    | JPA Repository                           |
|-------------------------|-----------------------------------------|-----------------------------------------|
| Definition              | Basic operations for data manipulation  | Abstraction layer for data persistence  |
| Manual vs Automatic      | Requires manual SQL queries             | Automatically generates queries          |
| Framework Dependency     | Not dependent on a specific framework   | Part of Spring Data framework            |
| Code Boilerplate        | More boilerplate code needed            | Reduces boilerplate with predefined methods |
| Method Naming           | Custom method implementation             | Method names determine query behavior    |
| Performance             | Direct control over SQL                 | May add some overhead due to abstraction |

## Conclusion
While CRUD is a set of operations applicable in any data management context, JPA Repository provides a higher-level abstraction specifically for Java applications, simplifying data access and management through automatic query generation.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // Additional query methods can be defined here if needed
}

```


## Question- Named query vs Native query
### Named Query vs Native Query

**Named Query:**
- **Definition:** A predefined query defined using annotations (`@NamedQuery`) or XML. It is associated with an entity and can be reused.
- **Usage:** Generally used for static queries that are defined at the compile-time and can be referenced by name.
- **Example:**
  ```java
  @Entity
  @NamedQuery(name = "User.findByName", query = "SELECT u FROM User u WHERE u.name = :name")
  public class User {
      // fields, getters, setters
  }

  // Usage in a repository
  List<User> users = entityManager.createNamedQuery("User.findByName", User.class)
                                  .setParameter("name", "John")
                                  .getResultList();
  ```
  
**Native Query:**
- **Definition:**  A query written in the native SQL dialect of the underlying database. It can leverage all database features.
- **Usage:** Used when the required query cannot be expressed using JPQL or when you want to optimize performance with database-specific features.
- **Example:**
  

```java
List<User> users = entityManager.createNativeQuery("SELECT * FROM users WHERE name = ?", User.class)
                                .setParameter(1, "John")
                                .getResultList();
```

**Key Differences**
**Flexibility**: Named queries are more limited to JPQL syntax, while native queries can use any SQL syntax supported by the database.
**Performance**: Native queries may provide better performance for complex queries, while named queries are easier to manage and refactor.
**Debugging**: Named queries can be easier to debug since they are defined in one place, whereas native queries are often embedded within the code.


## Question- Named Query vs Native Query
### Adding Pagination in Native Query

To implement pagination in a native query, you can use the `setFirstResult()` and `setMaxResults()` methods of the `Query` interface. These methods allow you to specify the starting index and the maximum number of results to return.

### Example Code

Here's an example of how to add pagination to a native query in a Spring Data JPA repository:

```java
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.persistence.Query;
import java.util.List;

@Repository
public class UserRepository {

    @PersistenceContext
    private EntityManager entityManager;

    @Transactional
    public List<User> findUsersWithPagination(int page, int size) {
        int offset = page * size; // Calculate the starting index
        Query query = entityManager.createNativeQuery("SELECT * FROM users", User.class);
        query.setFirstResult(offset);
        query.setMaxResults(size);
        return query.getResultList();
    }
}
```

**Parameters Passed from UI for Pagination**
When implementing pagination in a UI, you typically pass the following parameters:

Page Number: This indicates the current page the user is on. For example, if your pagination starts from 0, then the first page is 0, the second is 1, and so on.

Example: page=1 (This usually means the second page if starting from 0).

Page Size: This indicates how many items should be displayed per page.

Example: size=10 (This means that 10 records will be displayed per page).

Example UI Parameters
When making a request to the API endpoint for fetching paginated data, the URL might look like this:
**GET /api/users?page=1&size=10**



## Question- Given employee table has columns name, age and dept. Get list of employees by name.
### Named Query to Get List of All Employees by Name

To define a named query in JPA for retrieving all employees by their name, you can follow these steps:

1. **Define the Named Query in the Entity Class**: Annotate the `Employee` entity with the `@NamedQuery` annotation.

2. **Use the Named Query in the Repository**: Create a method in your repository to execute the named query.

### Example Code

#### Employee Entity with Named Query

```java
import javax.persistence.*;

@Entity
@NamedQueries({
    @NamedQuery(
        name = "Employee.findByName",
        query = "SELECT e FROM Employee e WHERE e.name = :name"
    )
})
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private int age;
    private String department;

    // Getters and Setters
}


import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    List<Employee> findByName(String name);
}


import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class EmployeeService {

    @Autowired
    private EmployeeRepository employeeRepository;

    public List<Employee> getEmployeesByName(String name) {
        return employeeRepository.findByName(name);
    }
}


List<Employee> employees = employeeService.getEmployeesByName("John Doe");

```


## Question- Add authentication and authorization to a simple endpoint SpringBoot

### Simple API with Authentication and Authorization in Spring Boot

This example demonstrates a simple REST API using Spring Boot, with JWT-based authentication and authorization.

#### 1. Dependencies

Add the following dependencies to your `pom.xml` for Spring Boot, Spring Security, and JWT:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt</artifactId>
        <version>0.9.1</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
            .withUser("user")
            .password(passwordEncoder().encode("password"))
            .roles("USER")
            .and()
            .withUser("admin")
            .password(passwordEncoder().encode("admin"))
            .roles("ADMIN");
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeRequests()
            .antMatchers("/api/public").permitAll()
            .antMatchers("/api/admin").hasRole("ADMIN")
            .anyRequest().authenticated()
            .and()
            .httpBasic();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}


import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class ApiController {

    @GetMapping("/api/public")
    public String publicEndpoint() {
        return "This is a public endpoint!";
    }

    @GetMapping("/api/admin")
    public String adminEndpoint() {
        return "This is an admin endpoint!";
    }
}

```

## Question- How @Autowired internally works

### How `@Autowired` Internally Works in Spring

The `@Autowired` annotation in Spring is used for dependency injection, allowing Spring to resolve and inject collaborating beans into your bean. Here’s how it works internally:

#### 1. **Spring Container and Bean Factory**

When the Spring application starts, the Spring container initializes and creates a bean factory. The container reads the configuration files (either XML or Java configuration classes) to identify the beans that need to be managed.

#### 2. **Bean Creation**

During the bean creation process, Spring instantiates the bean and identifies the dependencies required by the bean. It does this by examining the fields and constructor parameters annotated with `@Autowired`.

#### 3. **Dependency Resolution**

Once the Spring container identifies a bean that has dependencies marked with `@Autowired`, it tries to resolve these dependencies:

- **Type Matching**: Spring looks for beans of the same type as the dependency. If there is a single bean of that type in the container, Spring will inject it directly.
  
- **Qualifier**: If multiple beans of the same type exist, you can use the `@Qualifier` annotation to specify which bean should be injected.

- **Optional Dependencies**: If the `required` attribute of `@Autowired` is set to `false`, Spring will not throw an exception if the bean is not found. Instead, it will inject `null`.

#### 4. **Injection Point**

The injection can happen at the following points:

- **Field Injection**: The dependency is injected directly into the fields of the class.
  
  ```java
  @Autowired
  private MyService myService;

private MyService myService;

@Autowired
public void setMyService(MyService myService) {
    this.myService = myService;
}

private final MyService myService;

@Autowired
public MyController(MyService myService) {
    this.myService = myService;
}
``

### 5. Bean Lifecycle
After dependency injection, the Spring container may perform additional lifecycle operations, such as calling @PostConstruct methods if they are present.

### 6. Proxying
If the bean is marked as a Spring-managed bean, Spring can create a proxy around it for additional features like AOP (Aspect-Oriented Programming). This proxy can intercept method calls and apply cross-cutting concerns like transaction management or logging.


## Question- Use of rest template, how the communication works and how it works in case of failure or timeouts

### Use of RestTemplate in Spring

`RestTemplate` is a synchronous client provided by Spring Framework for making HTTP requests. It simplifies the process of consuming RESTful web services. Here’s how it works and how it handles failures or timeouts.

#### 1. **Basic Usage of RestTemplate**

To use `RestTemplate`, you typically create an instance and use it to make various types of HTTP requests (GET, POST, PUT, DELETE). Here's an example:

```java
import org.springframework.web.client.RestTemplate;

@RestController
public class MyController {

    private final RestTemplate restTemplate;

    public MyController(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    @GetMapping("/consume")
    public String consumeExternalApi() {
        String url = "https://api.example.com/data";
        String response = restTemplate.getForObject(url, String.class);
        return response;
    }
}
```
### 2. How Communication Works
Making a Request: When you call methods like getForObject(), postForObject(), etc., RestTemplate constructs the appropriate HTTP request based on the method parameters.
Sending the Request: It then sends the request over the network to the specified URL and waits for a response.
Receiving the Response: Once the response is received, RestTemplate deserializes the response body into the desired Java object.

### 3. Error Handling
In case of failures or timeouts, RestTemplate has built-in mechanisms to handle different scenarios:

Timeouts: You can configure timeouts for the requests using RequestFactory. For example:
```java
import org.springframework.http.client.HttpComponentsClientHttpRequestFactory;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

@Bean
public RestTemplate restTemplate() {
    CloseableHttpClient httpClient = HttpClients.custom()
            .setConnectionTimeToLive(1000, TimeUnit.MILLISECONDS)
            .build();

    HttpComponentsClientHttpRequestFactory factory = new HttpComponentsClientHttpRequestFactory(httpClient);
    factory.setConnectTimeout(5000); // Set connection timeout
    factory.setReadTimeout(5000);    // Set read timeout

    return new RestTemplate(factory);
}

```

Handling Exceptions: When a request fails (e.g., due to network issues, timeouts, or server errors), RestTemplate throws specific exceptions such as:

HttpClientErrorException: For 4xx client errors.
HttpServerErrorException: For 5xx server errors.
ResourceAccessException: For resource access issues (like connection timeouts).

```java
try {
    String response = restTemplate.getForObject(url, String.class);
} catch (HttpClientErrorException e) {
    // Handle client error (4xx)
} catch (HttpServerErrorException e) {
    // Handle server error (5xx)
} catch (ResourceAccessException e) {
    // Handle resource access issue (timeout, etc.)
}

```

### 4. Fallback Mechanisms
For more robust applications, especially in microservices architectures, consider using libraries like Spring Cloud Netflix Hystrix or Resilience4j to implement circuit breaker patterns and fallback mechanisms. This way, if a service is down, you can provide alternative responses without impacting the overall system performance.


## Question- Interface vs Abstract class

### Abstract Class vs Interface in Java

#### 1. **Abstract Class**

- **Definition**: An abstract class is a class that cannot be instantiated and is meant to be subclassed. It may contain abstract methods (methods without implementation) and methods with implementation.
- **Key Characteristics**:
  - Can have both **abstract methods** and **concrete methods** (methods with a body).
  - Can maintain **state** using instance variables.
  - Can have constructors.
  - Can have access modifiers for its methods and fields (private, protected, etc.).
  - Can extend only **one class** (single inheritance).
  
- **Example**:

```java
abstract class Animal {
    String name;

    // Abstract method
    abstract void makeSound();

    // Concrete method
    void sleep() {
        System.out.println(name + " is sleeping.");
    }
}
```

### 2. Interface
Definition: An interface is a contract that defines a set of methods a class must implement. It primarily contains abstract methods (before Java 8) but can also have default and static methods (from Java 8 onwards).
Key Characteristics:
Methods are implicitly public and abstract (before Java 8).
From Java 8 onwards, interfaces can have default methods (with implementation) and static methods.
Cannot maintain state (cannot have instance variables).
No constructors.
Supports multiple inheritance (a class can implement multiple interfaces).

```java
interface Animal {
    // Abstract method
    void makeSound();

    // Default method (Java 8+)
    default void sleep() {
        System.out.println("Animal is sleeping.");
    }
}

```

### 3. Key Differences
Aspect	Abstract Class	Interface
Methods	Can have both abstract and concrete methods	Only abstract methods (Java 7 and earlier). Java 8+ allows default and static methods.
Variables	Can have instance variables	Only constants (public static final)
Constructors	Can have constructors	No constructors
Inheritance	Can extend one class	Can implement multiple interfaces
Default Methods	Not allowed until Java 8+	Allowed from Java 8+
Access Modifiers	Can have any access modifier	Methods are public by default (for interfaces before Java 9)

### 4. Java 8+ Changes in Interfaces
Default Methods: Interfaces can now have methods with default implementation using the default keyword.
Static Methods: Interfaces can define static methods.

### 5. Java 14 Context
Java 14 continues to build on changes from earlier versions but has some additions:

Records (introduced in Java 14) are a new feature but unrelated directly to abstract classes or interfaces. They are used to create immutable data classes with minimal boilerplate code.

Example of a record:

public record Person(String name, int age) {}

### 6. When to Use Abstract Class vs Interface
Abstract Class: Use when you want to provide a common base class with both shared code and abstract methods. Suitable when classes share a close relationship.
Interface: Use when you want to define a contract for unrelated classes to implement, allowing multiple inheritance of behavior.


## Question- Single linked list and Doubly Linked list

### Single Linked List

#### Data Structure:
A **Single Linked List** is a linear data structure where each element, known as a **node**, contains two components:
1. **Data**: The value or information that the node holds.
2. **Pointer (Next)**: A reference (pointer) to the next node in the sequence.

The list starts with a **head** node, which is the first node of the list. Each node points to the next one until the last node, whose pointer to the next node is `null`, indicating the end of the list.

#### Structure:
```java
class Node {
    int data;       // Stores data
    Node next;      // Points to the next node

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

**Doubly Linked List**
**Data Structure:**
A Doubly Linked List is a more advanced version of a linked list where each node contains three components:

**Data:** The value or information that the node holds.
Pointer (Prev): A reference to the previous node in the sequence.
Pointer (Next): A reference to the next node in the sequence.
The head node is the first node, and the tail is the last node. The tail node's next pointer is null, and the head node's prev pointer is null.

```java
class DoublyNode {
    int data;           // Stores data
    DoublyNode prev;    // Points to the previous node
    DoublyNode next;    // Points to the next node

    DoublyNode(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

```


## Question-  What happens when duplicate primary key record is inserted using JPA

When a duplicate primary key record is inserted using JPA, it results in a PersistenceException or EntityExistsException, depending on the underlying database and the JPA provider (like Hibernate).

Detailed Explanation:
Primary Key Constraint: The primary key in a database uniquely identifies each record. It must be unique, and attempting to insert a duplicate value for a primary key will violate this constraint.
Exception Handling: JPA relies on the underlying database constraints, so when you try to insert an entity with a duplicate primary key, the database will reject the operation and throw an exception, which JPA translates to a PersistenceException or EntityExistsException.

```Java
//Handling of the situation
try {
    entityManager.persist(emp2);
} catch (PersistenceException e) {
    System.out.println("Duplicate primary key insertion detected: " + e.getMessage());
}

```

## Question- JTA usage. and its latest alternatives

### JTA: A Deep Dive
What is JTA?

JTA (Java Transaction API) is a Java API that defines a standard way for applications to manage distributed transactions across multiple resources, such as databases, message queues, and web services. It provides a high-level abstraction for transaction management, allowing developers to focus on their application logic without having to worry about the underlying transaction implementation details.

### Key Features of JTA:

Transaction demarcation: JTA provides methods for starting, committing, and rolling back transactions.
Transaction propagation: JTA allows transactions to be propagated across multiple resources and components within a distributed application.
Transaction isolation levels: JTA supports different isolation levels to control how transactions interact with each other.
Transaction synchronization: JTA ensures that transactions are synchronized across multiple resources to maintain data consistency.
JTA Architecture:

### JTA consists of two main components:

Transaction Manager: The transaction manager is responsible for coordinating transactions across multiple resources. It acts as a central authority for managing transaction boundaries, propagation, and synchronization.
Transaction Participant: Transaction participants are the resources that participate in transactions. They can be databases, message queues, web services, or other transactional resources.
### JTA Implementation:

JTA is typically implemented using a transaction manager provided by an application server or a standalone transaction manager. Some popular JTA implementations include:

JBoss Transaction Manager (JTM): A standalone transaction manager provided by Red Hat.
Atomikos Transaction Manager: A commercial transaction manager that can be used in various environments.
Narayana Transaction Manager: An open-source transaction manager that can be used in standalone applications or integrated with application servers.
Benefits of Using JTA:

Simplified transaction management: JTA provides a high-level API for managing transactions, reducing the complexity of distributed transaction management.
Portability: JTA-compliant applications can be deployed on different platforms and application servers without requiring significant modifications.
Interoperability: JTA allows applications to interact with different transactional resources in a consistent manner.
Improved reliability: JTA can help improve the reliability of distributed applications by ensuring that transactions are committed or rolled back consistently.
Code Example (Spring Boot):
```java
Java
@Configuration
public class DataSourceConfiguration {

    @Bean
    public DataSource dataSource() {
        AtomikosDataSourceBean dataSource = new AtomikosDataSourceBean();
        dataSource.setUniqueResourceName("myDataSource");   

        dataSource.setXaDataSourceClassName("com.mysql.cj.jdbc.MysqlXADataSource");
        // Set other data source properties
        return dataSource;
    }

    @Bean
    public JtaTransactionManager transactionManager() {
        BitronixTransactionManager transactionManager = new BitronixTransactionManager();
        transactionManager.setUniqueName("myTransactionManager");
        return transactionManager;
    }
}

@Service
@Transactional
public class MyService {

    @Autowired
    private MyRepository myRepository;

    public void doSomethingTransactional() {
        // Perform transactional operations
        myRepository.save(new MyEntity());
        // ...
    }
}
```
Use code with caution.

**Drawbacks of JTA:**

Complexity: JTA can be complex to configure and manage, especially in large-scale distributed systems.
Performance overhead: JTA can introduce performance overhead, especially for simple transactions.
Vendor lock-in: Some JTA implementations may be tied to specific application servers or vendors.
Latest Alternatives to JTA:

Sagas: Sagas provide a decentralized approach to managing distributed transactions, breaking them down into a series of local transactions.
Event Sourcing: Event sourcing stores a sequence of events that represent the history of an entity, allowing for replayability and eventual consistency.
Choosing the Right Approach:

The choice between JTA, Sagas, and Event Sourcing depends on your specific requirements and preferences. Consider factors such as complexity, performance, scalability, and the nature of your application's transactions.

In conclusion, JTA is a powerful tool for managing distributed transactions in Java applications. While it has its drawbacks, it remains a valuable option for many use cases, especially in enterprise environments and when integrating with legacy systems. By understanding the benefits and drawbacks of JTA and its alternatives, you can make informed decisions about how to manage transactions in your applications.


## Question- String Pool and its benefits
# String Pool and Immutability in Java

## String Pool

The String pool is a memory area within the Java Virtual Machine (JVM) that stores `String` objects. Its primary purpose is to optimize memory usage by avoiding the creation of multiple instances of the same `String` value.

### Why is the String pool used in Java?

- **Memory Efficiency**: When a new `String` object is created, the JVM first checks if a `String` with the same value already exists in the pool. If it does, the existing object is reused, preventing unnecessary memory allocation. This can significantly reduce memory consumption in applications that deal with a large number of strings.

- **Performance Optimization**: Comparing strings is a common operation in many applications. By using the String pool, the JVM can perform string comparisons more efficiently, as it can directly compare references instead of the actual string content.

- **Interning**: The String pool is used for string interning. This process involves creating a canonical representation of a `String` object, ensuring that there is only one instance of that string in the JVM. This can be useful for string comparison and other string-related operations.

## Immutability of String Objects in Java

`String` objects in Java are immutable, meaning their contents cannot be changed after they are created. This immutability has several benefits:

- **Thread Safety**: Immutable objects are inherently thread-safe, as multiple threads can safely access and share them without worrying about synchronization issues. This simplifies concurrent programming and reduces the risk of race conditions.

- **Caching**: Since `String` objects are immutable, they can be cached more efficiently. The JVM can cache frequently used strings, improving performance and reducing memory usage.

- **Security**: Immutability can help prevent security vulnerabilities, as it makes it difficult for malicious code to modify strings and exploit them for unauthorized access or code injection.

- **Predictability**: Immutable objects are easier to reason about and predict their behavior, making code more reliable and maintainable.

---

## In summary:
- The **String pool** is used in Java to optimize memory usage and performance by avoiding duplicate `String` objects.
- `String` objects are **immutable** to ensure thread safety, caching efficiency, security, and predictability.


## Question- SOAP vs Rest
# SOAP vs REST

## 1. **SOAP (Simple Object Access Protocol)**
- **Protocol**: SOAP is a protocol that defines strict standards for message format and communication.
- **Format**: XML is the only data format supported by SOAP.
- **Transport**: SOAP can work over any transport protocol, such as HTTP, SMTP, TCP, etc.
- **State**: SOAP is inherently **stateless** but can support stateful operations.
- **Security**: More complex but robust security options. It supports WS-Security for message encryption and authentication.
- **ACID Compliance**: Suitable for applications that require strict adherence to standards and formal contracts. Supports transactional operations, which makes it ideal for enterprise applications.
- **Error Handling**: Built-in error handling using SOAP Faults.
- **Usage**: Commonly used in legacy systems, financial services, or enterprise applications where security, reliability, and strict contracts are critical.

## 2. **REST (Representational State Transfer)**
- **Architecture Style**: REST is an architectural style that relies on stateless, client-server, cacheable communication.
- **Format**: REST can use multiple formats, such as JSON (most common), XML, YAML, and plain text.
- **Transport**: REST is typically used over HTTP.
- **State**: REST is **stateless**, meaning each request from the client contains all the information the server needs to fulfill the request.
- **Security**: Simpler security compared to SOAP. Authentication is usually done via OAuth, HTTPS, or other methods.
- **Performance**: Faster and more lightweight compared to SOAP since it uses JSON and avoids the overhead of strict protocols.
- **Scalability**: REST’s statelessness and ability to cache responses make it highly scalable.
- **Usage**: Commonly used for web services, mobile applications, and microservices due to its flexibility and performance.

---

## Question- Primary key in JPA
# Primary Key in JPA

## 1. **Definition**:
A **primary key** in JPA (Java Persistence API) is a unique identifier for an entity instance. It is used to ensure that each record in a database table can be uniquely identified.

## 2. **Annotations**:
JPA provides annotations to define the primary key for an entity.

- `@Id`: This annotation marks a field or property as the primary key of an entity.
- `@GeneratedValue`: It is used to indicate that the primary key value should be automatically generated. It supports several strategies:
  - `GenerationType.AUTO`: The persistence provider will pick an appropriate strategy (auto-increment, sequence, etc.).
  - `GenerationType.IDENTITY`: Uses database identity column.
  - `GenerationType.SEQUENCE`: Uses a sequence, which is a database object that generates numbers.
  - `GenerationType.TABLE`: Uses a table to generate unique values.

## 3. **Example**:
Here’s how to define a primary key in an entity class using JPA annotations:

```java
import javax.persistence.*;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private int age;

    // Constructors, Getters, Setters
}
```

### Composite Primary Key:
For tables with multiple primary keys (composite keys), JPA provides the @Embeddable and @EmbeddedId annotations.
```java
@Embeddable
public class EmployeeId implements Serializable {
    private Long employeeId;
    private Long departmentId;

    // Constructors, Getters, Setters
}

@Entity
public class Employee {

    @EmbeddedId
    private EmployeeId id;

    private String name;
    private int age;

    // Constructors, Getters, Setters
}

```


## Question- How json file upload happens to a rest api
In Spring Boot, you can accept a JSON file in the controller method by using the `@RequestBody` annotation

Otherwise if multipart file upload is required:-

```java
@PostMapping("/json")
    public String uploadJsonFile(@RequestParam("file") MultipartFile file) throws IOException {
        // Read the file content and process it
        String content = new String(file.getBytes());
        return "File uploaded with content: " + content;
    }
```

## Question - Kafka Topic Reading But Not Getting Consumed

When messages are being read from a Kafka topic but not consumed by the consumer, there can be several potential issues to investigate. Here are some common reasons and troubleshooting steps:

### 1. **Consumer Group Misconfiguration**
   - **Problem**: Kafka consumers are part of a consumer group. If multiple consumers in a group have the same group ID and are assigned the same partitions, only one consumer will receive messages from that partition.
   - **Solution**: Ensure that consumer groups are correctly configured. Each consumer in the group should be assigned to different partitions.

### 2. **Offset Mismanagement**
   - **Problem**: Kafka tracks the offset for each consumer. If the offset is not managed correctly, a consumer may be reading messages but not processing them because it's stuck on an old or already-processed offset.
   - **Solution**: Check the current offset of the consumer. If it's behind the latest offset, try resetting the offset using:
     - **Earliest**: Reset to the beginning of the topic.
     - **Latest**: Start from the most recent message.
   - This can be done via the `auto.offset.reset` property in the Kafka consumer configuration.

   Example:
   ```properties
   auto.offset.reset=earliest
```
# Kafka Topic Reading But Not Getting Consumed - Scenarios

1. **Consumer Group Misconfiguration**: Ensure unique group IDs for consumer groups.
2. **Offset Mismanagement**: Check and reset offsets if stuck on old ones.
3. **Partition Assignment Issues**: Ensure even distribution of partitions across consumers.
4. **Consumer Lag**: Monitor and address processing speed; scale consumers if needed.
5. **Consumer Not Polling Regularly**: Call `poll()` method frequently; avoid long processing times.
6. **Network or Connectivity Issues**: Check network settings and ensure broker-consumer connectivity.
7. **Dead Letter Queue (DLQ) Configuration**: Review logs for errors; ensure message processing is correct.
8. **Consumer Threading Issues**: Ensure thread-safe operations; simplify to single-threaded if debugging.
9. **Broker Configuration**: Check broker logs for replication or retention issues.
10. **Message Format or Schema Issues**: Ensure matching formats between producer and consumer.


## Question- What is zookeper and what it does with kafka. Steps in brief to implement it with kafka.

# What is ZooKeeper?

ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services in distributed systems. It acts as a coordinator for distributed applications.

## Role of ZooKeeper in Kafka

In the context of Apache Kafka, ZooKeeper serves the following purposes:

1. **Cluster Management**: Maintains the metadata of brokers in the Kafka cluster.
2. **Leader Election**: Manages leader election for Kafka partitions among brokers.
3. **Configuration Management**: Stores configuration data and provides information about topics, brokers, and consumers.
4. **Distributed Synchronization**: Ensures coordination between distributed processes.

## Steps to Implement ZooKeeper with Kafka

1. **Install ZooKeeper**: Download and install ZooKeeper on your machine or server.
   
2. **Configure ZooKeeper**: Edit the `zoo.cfg` configuration file to set data directories, client ports, and other settings.

3. **Start ZooKeeper Server**: Run the ZooKeeper server using the command:
   ```bash
   bin/zkServer.sh start
    ```
4.  **Download and Install Kafka**: Download and extract Kafka binaries.

5. **Configure Kafka to Use ZooKeeper** : In the server.properties file, set the zookeeper.connect property to point to your ZooKeeper instance:
zookeeper.connect=localhost:2181

6. **Start Kafka Server**: Run the Kafka server using the command:bin/kafka-server-start.sh config/server.properties
7. **Create topics**:-Use the Kafka command-line tools to create topics and start producing and consuming messages.
8. **Monitor**-: Use ZooKeeper commands to monitor the Kafka cluster, check broker status, and view topics.
   


## Question- What Happens if a Flow Breaks Down in a Transaction?

When a flow breaks down in a transaction, the behavior depends on how the transaction is managed. In Java and Spring frameworks, transactions typically follow the ACID properties (Atomicity, Consistency, Isolation, Durability). If the flow breaks down, the following can happen:

### 1. **Rollback**:
   - If a flow breaks (i.e., an exception occurs) during a transaction, the transaction is typically rolled back.
   - This means that all changes made during the transaction are reverted, and the database is returned to its previous state before the transaction began.
   - Rollback ensures **atomicity**, meaning either all operations in a transaction are completed successfully or none at all.

### 2. **Partial Updates Avoided**:
   - Transactions ensure that there are no **partial updates**. If the flow breaks down mid-way, none of the database operations committed so far will persist.
   - This helps in maintaining **consistency** in the system.

## 3. **Exception Handling**:
   - The application must handle the exception that caused the transaction to break. In Spring, this is typically done by throwing an exception from within the method annotated with `@Transactional`.

### 4. **Isolation of Transactions**:
   - Other concurrent transactions are not impacted by a broken transaction. They operate in **isolation**, and the failure of one transaction doesn’t impact others.

### 5. **Commit or Rollback**:
   - If the flow successfully completes without exceptions, the transaction is **committed**, and all changes are permanently written to the database.
   - If an error occurs, the transaction is **rolled back**, and no changes are persisted.

In Spring, the `@Transactional` annotation handles these scenarios, managing transaction boundaries and ensuring rollback on failure.



## Question- Difference Between `TRUNCATE` and `DELETE`

## 1. **Operation Type**:
   - **`DELETE`**: Deletes rows one at a time based on a specified condition (or all rows if no condition is given). It is a **DML (Data Manipulation Language)** operation.
   - **`TRUNCATE`**: Removes all rows from a table without logging individual row deletions. It is a **DDL (Data Definition Language)** operation.

## 2. **Condition Support**:
   - **`DELETE`**: You can delete specific rows using the `WHERE` clause (e.g., `DELETE FROM table WHERE condition`).
   - **`TRUNCATE`**: Cannot use conditions. It removes all rows in the table.

## 3. **Performance**:
   - **`DELETE`**: Slower, as each row deletion is logged for possible rollback.
   - **`TRUNCATE`**: Faster, as it doesn’t log individual row deletions and directly deallocates data pages.

## 4. **Rollback Capability**:
   - **`DELETE`**: Can be rolled back if executed within a transaction.
   - **`TRUNCATE`**: Cannot be rolled back once executed, as it doesn't log individual row deletions.

## 5. **Triggers**:
   - **`DELETE`**: Triggers associated with the table (like `BEFORE DELETE`, `AFTER DELETE`) are executed.
   - **`TRUNCATE`**: Triggers are not fired, as it doesn’t delete rows individually.

## 6. **Identity Reset**:
   - **`DELETE`**: Does not reset identity counters (e.g., auto-increment fields).
   - **`TRUNCATE`**: Resets identity counters back to their seed values.

## 7. **Locking**:
   - **`DELETE`**: Acquires row-level locks on the data.
   - **`TRUNCATE`**: Acquires a table-level lock.

In summary, use `DELETE` when you need fine-grained control or conditions on deletions, and use `TRUNCATE` for fast, bulk removal of all rows without logging.


## Question 2-Phase Commit (2PC)

**2-Phase Commit** is a distributed transaction protocol used to ensure that all participating nodes in a distributed system either commit or rollback a transaction, ensuring data consistency.

### Steps:
1. **Prepare Phase**:
   - The **coordinator** sends a `PREPARE` message to all participating nodes, asking them if they can commit.
   - Each **participant** checks if it can commit the transaction (e.g., checks local conditions like locks, etc.) and responds with either `YES` or `NO`.
   
2. **Commit Phase**:
   - If all participants respond with `YES`, the coordinator sends a `COMMIT` message, instructing all participants to commit the transaction.
   - If any participant responds with `NO`, the coordinator sends a `ROLLBACK` message, and all participants abort the transaction.

### Drawback:
- **Blocking**: If the coordinator fails during the commit phase, participants are left in an uncertain state, and they must wait until the coordinator recovers.

---

# 3-Phase Commit (3PC)

**3-Phase Commit (3PC)** is an improvement over the 2-Phase Commit, designed to reduce blocking and handle failures more gracefully by introducing an additional phase.

### Steps:
1. **CanCommit Phase**:
   - The coordinator sends a `CanCommit` request to all participants, asking if they can commit.
   - Participants reply with `YES` or `NO`.

2. **PreCommit Phase**:
   - If all participants respond `YES`, the coordinator sends a `PRECOMMIT` message, informing them to prepare for commit but not to finalize it yet.
   - Participants acknowledge that they are ready to commit.

3. **Commit Phase**:
   - The coordinator sends the final `COMMIT` message to commit the transaction, or a `ROLLBACK` if any participant was unable to commit earlier.

### Improvement:
- **Non-blocking**: In case of a coordinator failure, participants can safely make decisions based on timeouts or the PRECOMMIT phase.

---

### Key Difference:
- **2PC** can leave participants in an uncertain state if the coordinator crashes, whereas **3PC** adds an extra step to reduce this uncertainty and prevent indefinite waiting.


## Question- save and persist ways in JPA. explain about unique constraints.
# `save()` vs `persist()` in JPA related to Unique Constraints

In JPA, both `save()` and `persist()` methods are used to store entities in the database, but they differ in their behavior when handling unique constraints and entity states.

### 1. `save()` (Spring Data JPA)
- **Description**: The `save()` method is used in Spring Data JPA, typically when using `JpaRepository`. It works for both new and existing entities.
- **Handling Unique Constraints**:
  - When you call `save()`, it attempts to insert a new record if the entity is new. If an entity with the same unique constraint already exists, it throws a **constraint violation exception**.
  - If the entity already exists (determined by the ID), it performs an **update** rather than an insert.
  
- **Example**:
  ```java
  // Assuming there's a unique constraint on the 'email' field
  User user = new User("John", "john@example.com");
  userRepository.save(user); // inserts a new user

  // If another user with the same email exists, it violates the unique constraint
  User anotherUser = new User("Jane", "john@example.com");
  userRepository.save(anotherUser); // Throws constraint violation exception
  ```

### 2. persist() (EntityManager JPA)
**Description**: The persist() method is part of the EntityManager API and is used to make an entity managed and persist it to the database. It is specifically meant for new entities and cannot update existing entities.
Handling Unique Constraints:
When using persist(), if an entity violates a unique constraint (like a duplicate email), it also throws a constraint violation exception.
However, persist() cannot be used for updates. It will only insert new entities.

```java
User user = new User("John", "john@example.com");
entityManager.persist(user); // inserts a new user

// Trying to persist another user with the same email will violate the unique constraint
User anotherUser = new User("Jane", "john@example.com");
entityManager.persist(anotherUser); // Throws constraint violation exception

```
**Key Differences**
save():
Handles both insert and update operations.
Can be used with Spring Data JPA repositories.
Can violate unique constraints on both inserts and updates.
persist():
Only handles insert operations for new entities.
Can violate unique constraints on inserts only.
Part of the EntityManager API.


## Question - Query to find max salary
SELECT MAX(salary) AS maximum_salary
FROM employees;

## Question - Sum of employees salary grouped by department id
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;


## Question- Lifecycle of an Object in Java

In Java, an object's lifecycle consists of several stages, from its creation to its eventual destruction by the garbage collector. Here are the key phases in the lifecycle of an object:

### 1. Object Creation
- **Instantiation**: The object is created using the `new` keyword. Memory is allocated for the object in the heap.
    ```java
    MyObject obj = new MyObject();
    ```
- **Constructor Call**: After memory allocation, the constructor of the class is called to initialize the object’s fields and perform any setup tasks.
    ```java
    public MyObject() {
        // Initialize fields
    }
    ```

### 2. Object in Use
- **Reference**: The newly created object is referred to by a reference variable. Methods can be called on the object, and its state can be modified.
    ```java
    obj.someMethod();
    obj.someField = value;
    ```

### 3. Object Eligible for Garbage Collection
- **Dereferencing**: When there are no more references pointing to an object, it becomes **eligible** for garbage collection. This can happen when:
  - The reference is explicitly set to `null`.
    ```java
    obj = null;
    ```
  - The reference goes out of scope (e.g., method ends).
  
- **Garbage Collection**: Java's garbage collector automatically reclaims memory by destroying objects that are no longer reachable.

### 4. Object Finalization (Optional)
- **finalize()**: Before the object is collected by the garbage collector, its `finalize()` method may be called (if it is overridden). This gives the object a chance to release any resources (like file handles or network connections) before being destroyed.
    ```java
    @Override
    protected void finalize() throws Throwable {
        // Cleanup code
    }
    ```
  **Note**: The `finalize()` method is deprecated as of Java 9 due to inefficiency and unpredictability. Other cleanup mechanisms like `try-with-resources` are preferred.

### 5. Object Destruction
- Once the object is finalized (if needed), the garbage collector reclaims the memory and destroys the object, making the memory available for new objects.

### Summary:
- **Creation**: Using the `new` keyword, memory is allocated, and the constructor is called.
- **In Use**: The object is referenced and manipulated.
- **Garbage Collection**: When no longer referenced, the object becomes eligible for garbage collection.
- **Finalization (Optional)**: The `finalize()` method may be called for cleanup.
- **Destruction**: The object is destroyed, and its memory is reclaimed by the garbage collector.

This object lifecycle ensures efficient memory management in Java applications, allowing developers to focus on writing code without worrying about manual memory management.


## Question- Talk about Hibernate Cache

In Hibernate, caching plays a crucial role in improving the performance of the application by reducing the number of database hits. Hibernate provides two levels of caching:

### 1. First-Level Cache (Session Cache)
- **Scope**: Per session, which means it is associated with a single Hibernate session.
- **Default Cache**: It is automatically enabled in Hibernate. Every entity retrieved by a session is stored in the session cache.
- **Usage**: The first-level cache stores objects in memory during the life of the session. Any repeated calls to fetch the same entity within the same session will be served from the cache rather than hitting the database.
    - Example:
    ```java
    Session session = sessionFactory.openSession();
    Employee employee = session.get(Employee.class, 1); // Hits the DB
    Employee employeeAgain = session.get(Employee.class, 1); // Served from the cache
    ```

- **Session Flush**: When the session is flushed, changes made in the session (inserts, updates, deletes) are pushed to the database.

### 2. Second-Level Cache (SessionFactory Cache)
- **Scope**: Global for a session factory, meaning it can be shared across multiple sessions.
- **Not Enabled by Default**: Second-level cache needs to be explicitly configured.
- **Purpose**: The second-level cache stores entities across multiple sessions. It helps reduce the number of queries to the database by caching entities even after a session has been closed.
    - Providers: Hibernate supports various cache providers like:
        - EhCache
        - Infinispan
        - Redis
        - Hazelcast
        - Others

- **Enabling Second-Level Cache**:
    - Add provider dependency (e.g., EhCache):
    ```xml
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-ehcache</artifactId>
    </dependency>
    ```
    - Configure caching in `hibernate.cfg.xml`:
    ```xml
    <property name="hibernate.cache.use_second_level_cache">true</property>
    <property name="hibernate.cache.region.factory_class">org.hibernate.cache.ehcache.EhCacheRegionFactory</property>
    ```

    - Annotate entities to use the second-level cache:
    ```java
    @Entity
    @Cacheable
    @org.hibernate.annotations.Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
    public class Employee {
        @Id
        private int id;
        private String name;
    }
    ```

### 3. Query Cache (Optional)
- **Caching Query Results**: The query cache stores the result set of frequently executed queries. This can reduce the load on the database for queries with constant or similar result sets.
- **Enabling Query Cache**:
    ```xml
    <property name="hibernate.cache.use_query_cache">true</property>
    ```
    - Example of using query cache:
    ```java
    Query query = session.createQuery("from Employee");
    query.setCacheable(true);
    List<Employee> employees = query.list();
    ```

### Caching Strategies
1. **Read-Only**: Best suited for data that does not change, such as reference data.
2. **Read-Write**: Suitable for entities that may be modified. It ensures consistency between the cache and the database.
3. **Non-Strict Read-Write**: Allows concurrent modifications, but there's a risk of cache inconsistencies.
4. **Transactional**: Provides full transactional support with strict guarantees, typically used with JTA transactions.

### Summary:
- **First-Level Cache**: Per session, enabled by default, caches within a single session.
- **Second-Level Cache**: Global across sessions, must be explicitly configured, and caches entities across sessions.
- **Query Cache**: Caches query result sets to avoid frequent DB hits.
- **Caching Providers**: Hibernate supports various cache providers (EhCache, Infinispan, etc.), and appropriate caching strategies (read-only, read-write, etc.) should be chosen based on the use case.


## Question- JPA Internal Working

The **Java Persistence API (JPA)** provides a specification for object-relational mapping (ORM) in Java, allowing developers to manage relational data in applications using Java objects. JPA is not an implementation; instead, it defines a set of rules and guidelines that implementations like Hibernate, EclipseLink, and OpenJPA follow.

### Key Components of JPA

1. **Entity Manager**:
   - The `EntityManager` is responsible for managing the lifecycle of entities, including operations like persist, remove, merge, and find.
   - It's the interface through which the application interacts with the persistence context.

2. **Persistence Context**:
   - The persistence context is a cache (first-level cache) where entity instances are managed. The `EntityManager` manages this context.
   - If an entity is already in the persistence context, JPA avoids hitting the database and returns the cached entity instead.
   - Once an entity is in the persistence context, any changes to it are automatically synchronized with the database when a transaction is committed or the context is flushed.

3. **Entity**:
   - An entity is a lightweight, persistent domain object that is mapped to a database table using JPA annotations such as `@Entity`, `@Table`, `@Id`, etc.
   - Example:
   ```java
   @Entity
   @Table(name = "employee")
   public class Employee {
       @Id
       private Long id;
       private String name;
       private String department;
   }
   ```
**Persistence Unit**:
The persistence.xml file defines one or more persistence units. Each persistence unit defines a set of entity classes that are managed together.
This file contains configurations such as the database connection details and the JPA provider being used.

### JPA Life Cycle
**Entity Creation:**

When an entity is created, it's considered transient—not yet managed by the persistence context.
**Persistence (persist):**

When persist() is called on an entity, the entity moves from transient to managed state.
Managed entities are synchronized with the database during transaction commit or flush.

```java
EntityManager em = entityManagerFactory.createEntityManager();
em.getTransaction().begin();
Employee emp = new Employee();
emp.setName("John");
em.persist(emp); // Entity becomes managed
em.getTransaction().commit(); // Changes are flushed to the DB

```

4. **Merge (update):**

If an entity is detached from the persistence context (e.g., the session was closed), it can be merged back into the persistence context using merge().
5. **Remove (delete):**

An entity can be removed using the remove() method, and it transitions to the removed state.
The removal is propagated to the database when the transaction commits.
6. **Query Execution:**

Queries in JPA can be done using JPQL (Java Persistence Query Language) or native SQL queries.
Example of JPQL:
```java
String jpql = "SELECT e FROM Employee e WHERE e.department = :dept";
List<Employee> employees = em.createQuery(jpql)
                             .setParameter("dept", "HR")
                             .getResultList();

```

7. **Transaction Management:**

JPA typically works in the context of a transaction. Transactions can either be container-managed (e.g., in a Java EE environment) or application-managed (in Java SE).
The EntityManager interacts with the transaction boundaries, and changes to managed entities are automatically synchronized with the database at transaction commit.

### JPA in Action (Example)
**Entity Manager Factory Creation**: The EntityManagerFactory is created once and provides instances of EntityManager for interacting with the persistence context.
EntityManagerFactory emf = Persistence.createEntityManagerFactory("EmployeePersistenceUnit");

**Persisting an Entity**: When persisting an entity, the entity manager interacts with the persistence context and eventually the database.
```java
EntityManager em = emf.createEntityManager();
em.getTransaction().begin();
Employee employee = new Employee();
employee.setName("John Doe");
em.persist(employee);  // Employee is now in the persistence context
em.getTransaction().commit();  // Data is synchronized with the database

```

### Internal Process Breakdown
**Entity Mapping:** When an entity class is annotated with @Entity, the JPA provider (e.g., Hibernate) maps the entity fields to corresponding database table columns. This allows the EntityManager to interact with the database.

**Object-Relational Mapping (ORM):** The JPA provider translates the Java class operations into SQL statements. It performs CRUD (Create, Read, Update, Delete) operations based on entity mappings.

**Transaction Coordination:** The JPA provider manages transactions internally or through the use of external transaction managers (e.g., JTA). On transaction commit, the EntityManager flushes the persistence context to the database.

**Caching:**

JPA includes first-level caching by default in the EntityManager. This prevents repeated queries within a session for the same entity.
For more advanced caching, second-level caching is managed by the JPA provider (e.g., Hibernate with EhCache).


### Key Responsibilities
JPA

Provides standard annotations like @Entity, @Table, @Id, etc.
Specifies the API for managing persistence contexts and transactions.
Hibernate

Implements JPA and adds additional features like caching, batch processing, and lazy loading.
Provides configuration options and utilities for database connections.
Spring Data JPA

Offers a repository abstraction layer, making it easy to create CRUD operations.
Provides support for query methods derived from method names.
Allows the integration of various data sources through a unified approach.

```java
// JPA Entity with Hibernate Annotations
@Entity
@Table(name = "employees") // Specifies the table name
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Hibernate generates primary key values
    private Long id;

    @Column(name = "employee_name", nullable = false) // Maps to a specific column
    private String name;

    @Column(name = "department", nullable = false)
    private String department;

    // Getters and Setters
}

// Spring Data JPA Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    List<Employee> findByDepartment(String department);
}

// Service Layer
@Service
public class EmployeeService {
    @Autowired
    private EmployeeRepository employeeRepository;

    public List<Employee> getEmployeesByDepartment(String department) {
        return employeeRepository.findByDepartment(department);
    }
}

// Application Configuration for Hibernate
@Configuration
@EnableTransactionManagement // Enables transaction management
public class HibernateConfig {
    @Bean
    public LocalSessionFactoryBean sessionFactory() {
        LocalSessionFactoryBean sessionFactory = new LocalSessionFactoryBean();
        sessionFactory.setPackagesToScan("com.example.model"); // Package of the model classes
        sessionFactory.setDataSource(dataSource());
        sessionFactory.setHibernateProperties(hibernateProperties());
        return sessionFactory;
    }

    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/mydb");
        dataSource.setUsername("username");
        dataSource.setPassword("password");
        return dataSource;
    }

    private Properties hibernateProperties() {
        Properties properties = new Properties();
        properties.put("hibernate.dialect", "org.hibernate.dialect.MySQL5Dialect");
        properties.put("hibernate.show_sql", "true"); // Show SQL queries in console
        properties.put("hibernate.hbm2ddl.auto", "update"); // Auto-update schema
        return properties;
    }
}

```

## Question- How object connects to a table

# How an Object Connects Internally to a Table in JPA/Hibernate

## 1. Object-Relational Mapping (ORM)

ORM is the technique that allows you to map Java objects to database tables. In JPA and Hibernate, this is achieved through annotations and configurations.

## 2. Key Components

- **Entity Class**: A Java class annotated with `@Entity` represents a table in the database. Each instance of this class corresponds to a row in the table.
  
- **Annotations**: Common annotations include:
  - `@Table`: Specifies the table name.
  - `@Id`: Defines the primary key of the entity.
  - `@GeneratedValue`: Indicates how the primary key is generated.
  - `@Column`: Maps a field to a specific table column.

## 3. Example Entity Class

Here’s an example of an entity class that connects to a `employees` table:

```java
import javax.persistence.*;

@Entity
@Table(name = "employees") // Maps the class to the employees table
public class Employee {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Automatically generate primary key
    private Long id;

    @Column(name = "employee_name", nullable = false) // Maps to employee_name column
    private String name;

    @Column(name = "department", nullable = false)
    private String department;

    // Getters and Setters
}
```
### 4. Persistence Context
When you interact with the database, JPA/Hibernate uses a Persistence Context. This context acts as a first-level cache, managing the state of entity instances and their relationships.

Entity Manager: The main interface for interacting with the persistence context.
Lifecycle States:
Transient: The object is created but not associated with any persistence context.
Managed: The object is associated with a persistence context and is synchronized with the database.
Detached: The object is no longer managed, but its state is still available.
Removed: The object is marked for deletion.

### 5. Saving an Object
When you save an object, the following steps occur:

Creating the Entity Manager: An EntityManager is created, which interacts with the persistence context.

Begin Transaction: A transaction is started using EntityTransaction.

Persisting the Object: The object is persisted using the persist() method.

```java
EntityManager em = entityManagerFactory.createEntityManager();
EntityTransaction transaction = em.getTransaction();

transaction.begin();
Employee employee = new Employee();
employee.setName("John Doe");
employee.setDepartment("Engineering");
em.persist(employee); // This connects the object to the employees table
transaction.commit();

```

## Question- Stream vs parallel stream

# Difference Between Stream and Parallel Stream

In Java, both `Stream` and `Parallel Stream` are part of the Java Stream API introduced in Java 8, and they are used for processing sequences of elements. However, they have key differences in their execution models:

## 1. Execution Model

- **Stream**:
  - A `Stream` processes elements sequentially.
  - It processes the data in the order it appears in the source (e.g., a list).
  - It is generally suitable for simple operations where the order of processing matters.

- **Parallel Stream**:
  - A `Parallel Stream` utilizes multiple threads to process elements in parallel.
  - It divides the data into chunks and processes them concurrently, making use of available CPU cores.
  - This can improve performance for large datasets but may lead to unpredictable ordering.

## 2. Performance

- **Stream**:
  - The performance may be slower for large datasets, as it processes elements one at a time.
  
- **Parallel Stream**:
  - Typically offers better performance for large datasets as it leverages multi-core processors, but the actual performance gain depends on the size of the data, the complexity of the operation, and the overhead of managing threads.

## 3. Order of Execution

- **Stream**:
  - Preserves the order of elements; operations are executed in the same order as the source.

- **Parallel Stream**:
  - The order is not guaranteed. While it may still appear ordered, operations could be executed out of order due to concurrent processing.

## 4. Use Cases

- **Stream**:
  - Best for tasks that require ordered processing or operations on smaller datasets.
  - Example: Filtering a list of items where the order is significant.

- **Parallel Stream**:
  - Ideal for computationally intensive tasks on large datasets where order does not matter.
  - Example: Performing complex transformations on a large collection of data.

## 5. Example Code

### Using Stream

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> filteredNames = names.stream()
                                  .filter(name -> name.startsWith("A"))
                                  .collect(Collectors.toList());
```
### Using Stream

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> filteredNames = names.parallelStream()
                                   .filter(name -> name.startsWith("A"))
                                   .collect(Collectors.toList());

```

## Question- Query for Sum of Employee Salaries Using Streams

double totalSalary = employees.stream()
                                       .filter(employee -> employee.getSalary() > 100000)
                                       .mapToDouble(Employee::getSalary)
                                       .sum();



## Question- OOps conecpt

# OOP Concepts

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects," which can contain data and code: data in the form of fields (attributes or properties), and code in the form of procedures (methods or functions). Here are the four main concepts of OOP:

## 1. Encapsulation
- **Definition**: Encapsulation is the bundling of data and methods that operate on that data within a single unit or class. It restricts direct access to some of the object's components.
- **Benefits**: 
  - Protects object integrity by preventing outside interference.
  - Allows for data hiding and restricting access to sensitive information.
  
## 2. Inheritance
- **Definition**: Inheritance is a mechanism where one class (subclass or derived class) can inherit fields and methods from another class (superclass or base class).
- **Benefits**: 
  - Promotes code reusability and establishes a relationship between classes.
  - Allows for the creation of a hierarchical classification.

## 3. Polymorphism
- **Definition**: Polymorphism allows methods to do different things based on the object it is acting upon. It enables a single interface to represent different underlying forms (data types).
- **Types**: 
  - **Compile-time (Method Overloading)**: Multiple methods with the same name but different parameters.
  - **Run-time (Method Overriding)**: Subclass provides a specific implementation of a method that is already defined in its superclass.

## 4. Abstraction
- **Definition**: Abstraction is the concept of hiding the complex implementation details and showing only the essential features of the object. It can be achieved through abstract classes and interfaces.
- **Benefits**: 
  - Simplifies code and improves readability.
  - Reduces complexity by exposing only relevant parts of the object.

## Summary
These four principles of OOP—encapsulation, inheritance, polymorphism, and abstraction—form the foundation of object-oriented design and programming, enabling developers to create modular, reusable, and maintainable code.



## Question- Microservices design patterns
# Microservices Design Patterns

Microservices architecture is a way of developing software applications as a suite of small, independently deployable services. Here are some commonly used design patterns in microservices:

## 1. API Gateway
- **Description**: Acts as a single entry point for all client requests, routing them to the appropriate microservices.
- **Benefits**:
  - Simplifies client interactions.
  - Handles cross-cutting concerns like authentication, logging, and rate limiting.

## 2. Service Discovery
- **Description**: Mechanism to automatically detect and register microservices, enabling them to communicate with each other without hardcoded IP addresses.
- **Benefits**:
  - Enables dynamic scaling and load balancing.
  - Simplifies service-to-service communication.

## 3. Circuit Breaker
- **Description**: Prevents an application from repeatedly trying to execute an operation that's likely to fail, allowing for recovery and fallback methods.
- **Benefits**:
  - Improves application resilience.
  - Reduces latency by avoiding unnecessary calls.

## 4. Saga Pattern
- **Description**: Manages distributed transactions by breaking them into a series of smaller transactions, each with its own compensating actions.
- **Benefits**:
  - Maintains data consistency across multiple services.
  - Avoids the complexity of two-phase commits.

## 5. Event Sourcing
- **Description**: Stores the state of an application as a sequence of events rather than as a single current state.
- **Benefits**:
  - Provides a complete history of changes.
  - Allows for easy recovery and debugging.

## 6. CQRS (Command Query Responsibility Segregation)
- **Description**: Separates the handling of read and write operations, using different models for querying data and performing updates.
- **Benefits**:
  - Optimizes performance and scalability.
  - Allows for independent evolution of the read and write models.

## 7. Bulkhead
- **Description**: Isolates different components or services to prevent failures from propagating.
- **Benefits**:
  - Increases resilience by containing failures.
  - Improves stability under load.

## 8. Sidecar
- **Description**: Deploys auxiliary services alongside a primary service to provide features like monitoring, logging, or configuration.
- **Benefits**:
  - Decouples additional functionality from the core application logic.
  - Simplifies management of cross-cutting concerns.

## Summary
Microservices design patterns help in building scalable, resilient, and maintainable applications. By applying these patterns, developers can address various challenges associated with microservices architecture.



## Question- Internal working of System.gc

# How `System.gc()` Method Works Internally

The `System.gc()` method in Java is a suggestion to the Java Virtual Machine (JVM) to perform garbage collection. It’s important to note that calling `System.gc()` does not guarantee immediate garbage collection. Instead, it requests the JVM to consider running the garbage collector at its discretion. Here’s a breakdown of how it works internally:

## 1. Request for Garbage Collection
- When `System.gc()` is called, it sends a request to the JVM to perform garbage collection.
- This request is just a hint; the JVM may choose to ignore it based on its own internal algorithms and policies.

## 2. Garbage Collector Activation
- If the JVM decides to respond to the request, it activates the garbage collector.
- The garbage collector scans the heap memory for objects that are no longer reachable or referenced from the application.

## 3. Mark-and-Sweep Algorithm
- Most JVM implementations use a mark-and-sweep algorithm as part of the garbage collection process:
  - **Mark Phase**: The garbage collector identifies which objects are still reachable. It marks these objects as "live."
  - **Sweep Phase**: The garbage collector then sweeps through the heap, collecting all unmarked objects (those not reachable) and freeing their memory.

## 4. Memory Reclamation
- After the sweep phase, the memory occupied by unreachable objects is reclaimed, making it available for future allocations.

## 5. Finalization
- Before an object is garbage collected, the JVM may call its `finalize()` method (if overridden) to allow the object to release any resources. However, the use of `finalize()` is generally discouraged in favor of other resource management techniques like try-with-resources.

## 6. JVM Decisions
- The JVM has its own heuristics for determining when to perform garbage collection, which can be influenced by factors such as:
  - Heap memory usage
  - Allocation rates
  - The specific garbage collection algorithm being used (e.g., G1, CMS, Parallel GC)

## Summary
The `System.gc()` method is a way to suggest garbage collection, but it does not guarantee it. The actual garbage collection process is determined by the JVM, which uses various algorithms and heuristics to manage memory efficiently.



## Question- Why wait, notify methods are in Object class
# Why `wait()`, `notify()`, and `notifyAll()` Exist in the `Object` Class

## 1. Synchronization Mechanism
- The `wait()`, `notify()`, and `notifyAll()` methods are part of the Java synchronization mechanism.
- These methods facilitate communication between threads that share the same object. When a thread needs to wait for a certain condition to be true, it can call `wait()` on the object. When the condition is met, another thread can call `notify()` or `notifyAll()` on the same object to wake up waiting threads.

## 2. Object-Level Locking
- In Java, every object can act as a monitor (lock) for synchronization. This means that any object can be used for thread communication, not just instances of the `Thread` class.
- By placing these methods in the `Object` class, Java allows any object to utilize these synchronization features. This provides flexibility, as developers can synchronize on any shared resource.

## 3. Use Case Scenarios
- **Producer-Consumer Problem**: A classic use case where one thread produces data and another consumes it. The producer may need to wait if the buffer is full, and the consumer may need to wait if the buffer is empty.
- In this scenario, both threads share the same buffer object, allowing them to call `wait()` and `notify()` on it.

## 4. Simplicity and Flexibility
- By including these methods in the `Object` class, Java simplifies the implementation of thread communication. You can use any object for waiting and notification, rather than being constrained to a specific thread-based class.
- This design promotes cleaner and more modular code, where different parts of an application can communicate without being tightly coupled.

## Summary
- The `wait()`, `notify()`, and `notifyAll()` methods exist in the `Object` class to provide a synchronization mechanism that can be utilized by any object, not just threads. This design allows for flexible and efficient inter-thread communication while promoting modular and maintainable code.


## Question- Princials followed by springboot
# Principles Followed by Spring Boot Applications

Spring Boot applications are designed around several core principles that enhance their usability, maintainability, and performance. Here are some key principles:

## 1. Convention over Configuration
- **Description**: Spring Boot reduces the need for extensive configuration by providing default settings. Developers can override these defaults only when necessary.
- **Benefit**: This principle minimizes boilerplate code and speeds up development.

## 2. Dependency Injection
- **Description**: Spring Boot leverages the Inversion of Control (IoC) principle through dependency injection to manage application components.
- **Benefit**: This promotes loose coupling between components and makes the application easier to test and maintain.

## 3. Microservices Architecture
- **Description**: Spring Boot is well-suited for building microservices, where applications are broken down into smaller, independently deployable services.
- **Benefit**: This architecture allows for scalability, flexibility, and easier maintenance of individual components.

## 4. Embedded Servers
- **Description**: Spring Boot allows applications to run with embedded servers (like Tomcat, Jetty, or Undertow).
- **Benefit**: This simplifies deployment and makes it easier to create standalone applications.

## 5. Production-Ready Features
- **Description**: Spring Boot provides built-in features for application monitoring, health checks, and metrics via Actuator.
- **Benefit**: This supports operational needs, enabling easier management and monitoring of applications in production.

## 6. Opinionated Defaults
- **Description**: Spring Boot comes with pre-defined conventions and default configurations based on best practices.
- **Benefit**: This helps developers get started quickly without worrying about making every decision from scratch.

## 7. Configurable
- **Description**: Spring Boot allows for easy externalized configuration, enabling properties to be set via various sources (e.g.,


## Question- When to use String, StringBuffer, StringBuilder
# When to Use String, StringBuffer, and StringBuilder

Java provides three classes for handling strings: `String`, `StringBuffer`, and `StringBuilder`. Each has its own use cases based on mutability, thread-safety, and performance. Here’s when to prefer each:

## 1. String
- **Description**: `String` is immutable, meaning once created, its value cannot be changed.
- **When to Use**:
  - When you need a constant string or a string that does not change.
  - For performance with small, infrequent string manipulations (concatenation).
  - When working with string literals or fixed strings.
  
### Example Use Case:
```java
String greeting = "Hello, World!";
```
### 2. StringBuffer
Description: StringBuffer is mutable and synchronized, making it thread-safe.
**When to Use:**
When working in a multi-threaded environment where multiple threads may modify the same string.
When you need to perform frequent modifications (e.g., appending, inserting) to a string.
```java
StringBuffer sb = new StringBuffer("Hello");
sb.append(", World!");
```
### 3. StringBuilder
Description: StringBuilder is mutable but not synchronized, making it more efficient than StringBuffer for single-threaded applications.
**When to Use:**
When you are working in a single-threaded environment or when thread safety is not a concern.
When you need to perform numerous string manipulations (concatenation, insertion) for better performance.
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(", World!");
```


## Question- When to use hashtable and hashMap

# When to Use HashMap and Hashtable

Both `HashMap` and `Hashtable` are implementations of the `Map` interface in Java, but they have distinct characteristics and use cases. Here's a comparison to help you decide when to use each.

## 1. HashMap
- **Description**: `HashMap` is part of the Java Collections Framework. It is a mutable, non-synchronized collection that allows null keys and values.
- **When to Use**:
  - When you need a map that allows null keys and values.
  - In single-threaded applications where thread safety is not a concern.
  - For better performance in scenarios where synchronization is not required.
  
### Example Use Case:
```java
HashMap<String, Integer> map = new HashMap<>();
map.put("Alice", 30);
map.put("Bob", 25);
```
### 2. Hashtable
Description: Hashtable is an older implementation that is synchronized, meaning it is thread-safe. It does not allow null keys or values.
**When to Use:**
In multi-threaded applications where you need to ensure thread safety without additional synchronization mechanisms.
When working with legacy code that requires Hashtable.
If you want to prevent null keys and values.
```java
Hashtable<String, Integer> table = new Hashtable<>();
table.put("Alice", 30);
table.put("Bob", 25);

```

## Question- HTTP methods

# Types of REST API Methods

REST (Representational State Transfer) APIs use standard HTTP methods to perform operations on resources. Here are the primary HTTP methods used in REST APIs, along with their typical use cases.

## 1. GET
- **Description**: Retrieves data from the server.
- **When to Use**:
  - When you want to fetch resources without modifying them.
  - For operations where you need to read data (e.g., getting user details, fetching a list of items).

## 2. POST
- **Description**: Sends data to the server to create a new resource.
- **When to Use**:
  - When you need to create a new resource (e.g., adding a new user, submitting a form).
  - For operations that result in a change on the server side.

## 3. PUT
- **Description**: Updates an existing resource or creates it if it does not exist.
- **When to Use**:
  - When you need to update a complete resource (e.g., updating user details).
  - For idempotent operations where multiple identical requests have the same effect as a single request.

## 4. PATCH
- **Description**: Partially updates an existing resource.
- **When to Use**:
  - When you need to modify only specific fields of a resource (e.g., updating just the email address of a user).
  - For scenarios where a full resource update is not required.

## 5. DELETE
- **Description**: Removes a resource from the server.
- **When to Use**:
  - When you need to delete an existing resource (e.g., removing a user or an item).
  - For operations that require resource removal.

## Summary
- **GET**: Use to retrieve data.
- **POST**: Use to create new resources.
- **PUT**: Use to update or create resources.
- **PATCH**: Use to partially update resources.
- **DELETE**: Use to remove resources.



## Quesiton- Why we dont prefer put for insert
# Why We Don't Prefer to Use PUT Mapping for Insert Operations

In RESTful APIs, the distinction between `PUT` and `POST` methods is essential for defining resource manipulation correctly. Here's why using `PUT` for insert operations is generally not preferred:

## 1. Idempotence
- **Definition**: An operation is idempotent if making the same request multiple times has the same effect as making it once.
- **Issue with PUT**: 
  - `PUT` is designed to be idempotent. If you send the same `PUT` request multiple times, it should not create multiple resources. Instead, it should only create or update the resource at a specific URI.
  - Using `PUT` for insertions can lead to confusion, as sending the same `PUT` request repeatedly could overwrite the resource instead of creating it.

## 2. Resource URI
- **Expectation**: When using `PUT`, the client typically knows the URI of the resource to be created or updated.
- **Issue with PUT**: 
  - In an insertion scenario, the server usually generates the resource's URI (e.g., for a new user). This is more aligned with `POST`, where the server creates the resource and returns its URI.

## 3. Semantics
- **HTTP Semantics**: `POST` is semantically intended for creating resources, while `PUT` is for updating existing resources or creating resources at a specific location.
- **Best Practice**: Following RESTful principles, `POST` should be used for creating new resources to avoid misinterpretation of the API's behavior.

## Summary
- **Idempotence**: `PUT` is idempotent, while `POST` is not, making `POST` a better choice for insert operations.
- **Resource URI**: `POST` allows the server to determine the resource's URI, while `PUT` requires the client to specify it.
- **Semantic Clarity**: Using `POST` for creation aligns with HTTP semantics, leading to clearer and more predictable API behavior.



## Question- Difference Between StackOverflowError and OutOfMemoryError

In Java, `StackOverflowError` and `OutOfMemoryError` are both subclasses of `Error`, indicating serious issues that can occur during the execution of a program. Here’s a comparison of the two:

## 1. Definition
- **StackOverflowError**:
  - This error occurs when a thread's stack size exceeds its allocated limit, typically due to deep or infinite recursion.
  - It indicates that the call stack has reached its maximum depth and can no longer accept more method calls.

- **OutOfMemoryError**:
  - This error occurs when the Java Virtual Machine (JVM) cannot allocate memory for an object, usually because the heap memory is exhausted.
  - It can happen for various reasons, including memory leaks, large data structures, or insufficient memory allocation.

## 2. Cause
- **StackOverflowError**:
  - Caused primarily by excessive recursion or a very deep call stack.
  - Example: A method calling itself indefinitely without a proper base case.

- **OutOfMemoryError**:
  - Caused by insufficient memory allocation for the heap, or when the application consumes more memory than is available.
  - Example: Holding large collections in memory or creating too many objects without releasing them.

## 3. Impact
- **StackOverflowError**:
  - Typically leads to the termination of the thread that caused it, but other threads may continue to run.
  - It often indicates a flaw in the code, such as poor recursion design.

- **OutOfMemoryError**:
  - Can affect the entire JVM, potentially leading to the termination of the application if no memory is available to allocate.
  - It signals a broader memory management issue that might require a review of the application’s memory usage.

## 4. Resolution
- **StackOverflowError**:
  - Refactor code to reduce recursion depth or use iteration instead of recursion when possible.
  - Ensure that recursive methods have proper base cases.

- **OutOfMemoryError**:
  - Analyze memory usage and identify memory leaks or inefficient memory consumption.
  - Consider increasing the JVM heap size or optimizing the application to reduce memory requirements.

## Summary
- `StackOverflowError` is related to the stack size and deep recursion, while `OutOfMemoryError` is related to heap memory exhaustion.
- Both errors indicate critical problems in the application, but they arise from different causes and require different approaches for resolution.


## Question- How to disable tomcat in springboot

# Disabling Tomcat in a Spring Boot Application

## Method 1: Exclude Tomcat Dependency

If you want to create a Spring Boot application without the embedded Tomcat server, you can exclude the Tomcat dependency from your `pom.xml` or `build.gradle`.

### For Maven

Add the following dependency in your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
//then add depedency of other server, like netty
```
Set server to invalid value, tomcat will not start
server.port=-1


## Question- DI vs IOC

# Dependency Injection vs. Inversion of Control

## Inversion of Control (IoC)

**Definition**: Inversion of Control is a design principle where the control of object creation and management is transferred from the application to a container or framework. This means that instead of the application code controlling the flow and lifecycle of objects, the control is inverted to a framework.

**Characteristics**:
- **Loose Coupling**: IoC promotes loose coupling between components, making it easier to manage and test them independently.
- **Framework Driven**: The framework (like Spring) manages the life cycle of application components, instantiating and configuring them as needed.
- **Flexibility**: Changes in implementation do not require modifications in the code that uses the components.

**Example**: A typical IoC scenario is a web application where the framework handles the request and response lifecycle, invoking the appropriate business logic classes.

## Dependency Injection (DI)

**Definition**: Dependency Injection is a specific implementation of the Inversion of Control principle. It allows a class to receive its dependencies from an external source rather than creating them itself. DI can be achieved through constructor injection, setter injection, or method injection.

**Characteristics**:
- **Dependencies Provided Externally**: DI provides the dependencies a class needs through its constructor, setter methods, or other means, promoting better separation of concerns.
- **Types of Injection**:
  - **Constructor Injection**: Dependencies are provided through the class constructor.
  - **Setter Injection**: Dependencies are provided through setter methods.
  - **Interface Injection**: Dependencies are provided through methods defined in an interface that the dependent class implements.

**Example**: In a Spring application, a service class can be injected with a repository dependency using annotations like `@Autowired`, allowing the framework to manage the instantiation of the repository class.

## Summary

- **Inversion of Control** is a broader design principle that encompasses various techniques for transferring control from the application to the framework.
- **Dependency Injection** is a specific technique used to implement IoC, focusing on how dependencies are supplied to classes.

### Key Differences

| Aspect                   | Inversion of Control                     | Dependency Injection                     |
|--------------------------|-----------------------------------------|------------------------------------------|
| **Definition**           | A design principle                      | A specific implementation of IoC        |
| **Focus**                | Control flow and lifecycle management   | Providing dependencies to classes        |
| **Mechanism**            | Can use various patterns                 | Primarily uses injection methods         |
| **Usage**                | General application design               | Specific to dependency management        |

By understanding both concepts, developers can design more modular, testable, and maintainable applications.


## Question- Creating Index for Composite Key in MongoDB

In MongoDB, you can create a composite index on multiple fields to optimize queries that filter on those fields. Here’s how to create a composite index for a composite key.

## Steps to Create Composite Index

### 1. Define the Composite Key

Identify the fields that will make up the composite key. For example, let's say you have a collection named `employees` with fields `employeeId` and `departmentId`.

### 2. Use the `createIndex` Method

You can create the index using the `createIndex` method. Below is an example of how to create a composite index on the `employeeId` and `departmentId` fields.

### Example Code

```javascript
db.employees.createIndex(
    { employeeId: 1, departmentId: 1 } // 1 for ascending order
)
```
### 3. Verify the Index
db.employees.getIndexes()

### 4. Querying with Composite Index
db.employees.find({ employeeId: 12345, departmentId: "Sales" })


## Question- How Partitioning Works in Kafka

Apache Kafka is a distributed event streaming platform that uses a concept called **partitioning** to ensure high availability, scalability, and fault tolerance of messages. Here’s an overview of how partitioning works in Kafka:

## 1. Definition of Partition

A **partition** is a smaller, ordered segment of a Kafka topic. Each topic in Kafka can have one or more partitions, allowing it to scale horizontally. Each partition is an immutable sequence of records that is continually appended to, and messages within a partition are assigned a unique offset.

## 2. Partitioning Strategy

When a producer sends messages to a Kafka topic, it must determine which partition the message will go to. Kafka provides several ways to determine this:

### a. Round Robin

- Messages are distributed evenly across all partitions in a round-robin fashion.
- This is the default behavior when no partition key is specified.

### b. Partition Key

- Producers can specify a partition key when sending a message.
- Kafka uses a hashing algorithm to determine the partition based on the key. This ensures that all messages with the same key will go to the same partition, preserving the order of those messages.

### c. Custom Partitioning

- Developers can implement their own partitioning logic by implementing the `Partitioner` interface.
- This allows for more sophisticated strategies based on application requirements.

## 3. Message Ordering

- Within each partition, messages are stored in the order they are received.
- Kafka guarantees that messages sent to the same partition will be read in the order they were produced.
- However, there is no guarantee of message ordering across different partitions.

## 4. Scalability and Fault Tolerance

### a. Horizontal Scalability

- By distributing messages across multiple partitions, Kafka can handle more data and high throughput.
- Each partition can be hosted on different brokers, allowing for load balancing.

### b. Replication

- Partitions can be replicated across multiple brokers for fault tolerance.
- Each partition has one leader and multiple replicas. The leader handles all read and write requests, while the replicas ensure data availability in case of broker failure.

## 5. Consumer Groups and Partition Assignment

- Consumers in Kafka can join a **consumer group** to share the workload.
- Each partition in a topic can be consumed by only one consumer within a group at a time, ensuring that messages are processed once and only once.

### Partition Assignment Strategies:

- **Range Assignment**: Each consumer gets a contiguous range of partitions.
- **Round Robin Assignment**: Partitions are distributed evenly among consumers.
- **Sticky Assignment**: Tries to minimize partition movements when rebalancing.

## Summary

- **Partitions**: Ordered segments of a topic, allowing for scalability and parallel processing.
- **Partitioning Strategy**: Messages can be distributed via round robin, partition keys, or custom logic.
- **Ordering**: Guaranteed within partitions, but not across them.
- **Scalability & Fault Tolerance**: Achieved through replication and distribution of partitions.
- **Consumer Groups**: Facilitate load balancing among consumers while ensuring message processing guarantees.

Understanding how partitioning works in Kafka is crucial for designing effective messaging systems that leverage Kafka’s capabilities for high throughput and reliability.

