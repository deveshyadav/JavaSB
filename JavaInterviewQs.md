Question 1: Java 8 features
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
