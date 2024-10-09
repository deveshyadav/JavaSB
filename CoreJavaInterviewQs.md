## Concurrent java collections
### 1. ConcurrentHashMap
Usage: A thread-safe variant of HashMap. It allows concurrent access and updates to the map without locking the entire collection.
Key Feature: Uses segmentation to lock only a portion of the map, improving performance in high-concurrency situations.
```java
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentMapExample {
    public static void main(String[] args) {
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();

        // Adding elements
        map.put("A", 1);
        map.put("B", 2);

        // Concurrent update
        map.computeIfAbsent("C", key -> 3);

        // Iterating over the map
        map.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}
```

### 2. CopyOnWriteArrayList
Usage: A thread-safe version of ArrayList. It creates a copy of the array on every write operation (e.g., add, set), making it ideal for scenarios where reads are more frequent than writes.
Key Feature: Ensures no locks are required during read operations, making it very fast for read-heavy operations.

```java
import java.util.concurrent.CopyOnWriteArrayList;

public class CopyOnWriteArrayListExample {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();

        // Adding elements
        list.add("Hello");
        list.add("World");

        // Reading elements
        list.forEach(System.out::println);

        // Write operation creates a new copy of the list
        list.add("Concurrent");
        list.forEach(System.out::println);
    }
}
```

### 3. ConcurrentLinkedQueue
Usage: A non-blocking queue based on linked nodes. It is useful when multiple threads share a queue, and thread contention should be minimized.
Key Feature: Implements a lock-free algorithm for high-performance concurrent access.
```java
import java.util.concurrent.ConcurrentLinkedQueue;

public class ConcurrentQueueExample {
    public static void main(String[] args) {
        ConcurrentLinkedQueue<String> queue = new ConcurrentLinkedQueue<>();

        // Adding elements
        queue.offer("Task1");
        queue.offer("Task2");

        // Polling (removing) elements
        System.out.println(queue.poll()); // Task1
        System.out.println(queue.poll()); // Task2
    }
}
```

### 4. BlockingQueue (e.g., ArrayBlockingQueue, LinkedBlockingQueue)
Usage: A thread-safe queue where threads can block (wait) while trying to add or remove elements when the queue is full or empty.
Key Feature: Useful in producer-consumer scenarios where one thread produces data and another thread consumes it.
```java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

public class BlockingQueueExample {
    public static void main(String[] args) throws InterruptedException {
        BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);

        // Producer Thread
        new Thread(() -> {
            try {
                queue.put("Data1");
                queue.put("Data2");
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }).start();

        // Consumer Thread
        new Thread(() -> {
            try {
                System.out.println(queue.take()); // Data1
                System.out.println(queue.take()); // Data2
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }).start();
    }
}
```

### 5. ConcurrentSkipListMap
Usage: A thread-safe, scalable, and ordered version of TreeMap based on a skip-list. It maintains keys in sorted order.
Key Feature: Ideal when you need both ordering and concurrency.
```java
import java.util.concurrent.ConcurrentSkipListMap;

public class SkipListMapExample {
    public static void main(String[] args) {
        ConcurrentSkipListMap<String, Integer> skipListMap = new ConcurrentSkipListMap<>();

        // Adding elements
        skipListMap.put("Key1", 100);
        skipListMap.put("Key2", 200);

        // Iterating through keys in sorted order
        skipListMap.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}
```

### 6. CopyOnWriteArraySet
Usage: A thread-safe version of HashSet that uses CopyOnWriteArrayList internally. Best suited for read-heavy scenarios where few updates are performed.
Key Feature: All mutative operations result in creating a new copy of the array.
```java
import java.util.concurrent.CopyOnWriteArraySet;

public class CopyOnWriteArraySetExample {
    public static void main(String[] args) {
        CopyOnWriteArraySet<String> set = new CopyOnWriteArraySet<>();

        // Adding elements
        set.add("Hello");
        set.add("World");

        // Reading elements
        set.forEach(System.out::println);

        // Write operation creates a new copy
        set.add("Concurrent");
        set.forEach(System.out::println);
    }
}
```


# RestTemplate and WebClient Methods

## RestTemplate Methods

1. **`getForObject(String url, Class<T> responseType, Object... uriVariables)`**
   - Retrieves a representation by doing a GET on the specified URL.

2. **`getForEntity(String url, Class<T> responseType, Object... uriVariables)`**
   - Retrieves an entity by doing a GET on the specified URL.

3. **`postForObject(String url, Object request, Class<T> responseType, Object... uriVariables)`**
   - Creates a new resource by POSTing the given object to the specified URL.

4. **`postForEntity(String url, Object request, Class<T> responseType, Object... uriVariables)`**
   - Creates a new resource and returns the response entity.

5. **`put(String url, Object request, Object... uriVariables)`**
   - Updates a resource by doing a PUT on the specified URL.

6. **`delete(String url, Object... uriVariables)`**
   - Deletes the resource at the specified URL.

7. **`exchange(String url, HttpMethod method, HttpEntity<?> requestEntity, Class<T> responseType, Object... uriVariables)`**
   - Executes a specified HTTP method against the specified URL.

8. **`headForHeaders(String url, Object... uriVariables)`**
   - Retrieves the headers for the resource at the specified URL.

9. **`optionsForAllow(String url, Object... uriVariables)`**
   - Retrieves the HTTP methods that are supported at the specified URL.

## WebClient Methods

1. **`get()`**
   - Initiates a GET request.

2. **`post()`**
   - Initiates a POST request.

3. **`put()`**
   - Initiates a PUT request.

4. **`delete()`**
   - Initiates a DELETE request.

5. **`exchange()`**
   - Executes a request with a specified method and returns a response.

6. **`uri(String uriTemplate, Object... uriVariables)`**
   - Sets the URI for the request.

7. **`bodyValue(T body)`**
   - Sets the body of the request.

8. **`retrieve()`**
   - Initiates the request and prepares to handle the response.

9. **`header(String headerName, String... headerValues)`**
   - Adds headers to the request.

10. **`accept(MediaType... acceptableMediaTypes)`**
    - Sets the Accept header for the response.

11. **`timeout(Duration timeout)`**
    - Sets a timeout for the request.

12. **`exchangeToMono(Function<ClientResponse, Mono<T>> responseMapper)`**
    - Maps the response to a Mono.

## Summary
- `RestTemplate` is a synchronous client and is more straightforward to use for simple requests.
- `WebClient` is a reactive, non-blocking client that is more suitable for modern applications requiring asynchronous processing.
- 

## Collection implementation scenario Questions

```java

//Count Employees by Department
  Map<String, Long> employeeCountByDepartment = employees.stream()
                                                             .collect(Collectors.groupingBy(Employee::getDepartment, Collectors.counting()));

// Get Distinct Departments
Set<String> distinctDepartments = employees.stream()
                                                  .map(Employee::getDepartment)
                                                  .collect(Collectors.toSet());

//Sort Employees by Name
List<Employee> sortedEmployees = employees.stream()
                                                  .sorted((e1, e2) -> e1.name.compareTo(e2.name))
                                                  .collect(Collectors.toList());

//Calculate Average Salary
double averageSalary = employees.stream().mapToDouble(Employee::getSalary).average().orElse(0);

//Find Employee with Maximum Salary
Employee maxSalaryEmployee = employees.stream()
                                              .max(Comparator.comparing(Employee::getSalary))
                                              .orElse(null);

//Group Employees by Salary Range
 Map<String, List<Employee>> employeesBySalaryRange = employees.stream()
            .collect(Collectors.groupingBy(emp -> {
                if (emp.getSalary() < 50000) return "<50k";
                else if (emp.getSalary() >= 50000 && emp.getSalary() <= 70000) return "50k-70k";
                else return ">70k";
            }));


//Convert List of Employees to a Map
 Map<String, Double> employeeMap = employees.stream()
            .collect(Collectors.toMap(Employee::getName, Employee::getSalary));

//Chaining Optional
String firstEmployeeName = service.getDepartment()
            .flatMap(department -> department.getEmployees().stream().findFirst())
            .map(Employee::getName)
            .orElse("No employees found");


```


## Common Java Exceptions

### General Exceptions

1. **NullPointerException**  
   Occurs when an application attempts to use an object reference that has the `null` value.

2. **ArrayIndexOutOfBoundsException**  
   Thrown to indicate that an array has been accessed with an illegal index, i.e., the index is negative or greater than or equal to the size of the array.

3. **ClassCastException**  
   Occurs when an object is cast to a subclass of which it is not an instance.

4. **ArithmeticException**  
   Thrown when an exceptional arithmetic condition has occurred, such as division by zero.

5. **IllegalArgumentException**  
   Indicates that a method has been passed an illegal or inappropriate argument.

6. **IllegalStateException**  
   Signals that a method has been invoked at an illegal or inappropriate time.

7. **NumberFormatException**  
   Thrown when an attempt to convert a string to a numeric type fails because the string does not have an appropriate format.

8. **IOException**  
   Signals that an I/O exception of some sort has occurred. This is a checked exception.

9. **FileNotFoundException**  
   A subclass of `IOException`, thrown when an attempt to open the file denoted by a specified pathname has failed.

10. **EOFException**  
    Thrown when an end of file or end of stream has been reached unexpectedly during input.

11. **SocketException**  
    Indicates an error occurred while creating or accessing a `Socket`.

12. **InterruptedException**  
    Thrown when a thread is waiting, sleeping, or otherwise occupied, and another thread interrupts it.

13. **StackOverflowError**  
    Thrown when a stack overflow occurs because an application recurses too deeply.

14. **OutOfMemoryError**  
    Signals that the Java Virtual Machine cannot allocate an object because it is out of memory and has no more memory to give.

15. **SecurityException**  
    Indicates a security violation has occurred, typically when a security manager is present and the requested operation is not allowed.

16. **ClassNotFoundException**  
    Thrown when an application tries to load a class through its string name but cannot find its definition.

17. **InvocationTargetException**  
    Thrown when an invoked method or constructor throws an exception.

18. **IndexOutOfBoundsException**  
    Signals that an index of some sort (e.g., in a string or array) is out of the allowable range.

19. **MalformedURLException**  
    Indicates that a malformed URL has occurred.

20. **SQLException**  
    Signals that a database access error or other errors occur when working with JDBC.

21. **ParseException**  
    Indicates that an error has occurred while parsing a string.

22. **UnsupportedClassVersionError**  
    Thrown when a class has been compiled with a more recent version of the Java Runtime Environment than the currently running JRE.

### Collection-Related Exceptions

23. **ConcurrentModificationException**  
    Occurs when a collection is modified while it is being iterated, except through the iterator's own remove method.

24. **NoSuchElementException**  
    Thrown by various accessor methods to indicate that the requested element does not exist.

25. **UnsupportedOperationException**  
    Signals that the requested operation is not supported, typically in the context of a collection.

### Bean-Related Exceptions

26. **BeanCreationException**  
    Thrown when a bean cannot be created in a Spring context.

27. **NoSuchBeanDefinitionException**  
    Indicates that a bean definition cannot be found in the Spring application context.

28. **UnsatisfiedDependencyException**  
    Thrown when a bean has an unsatisfied dependency that cannot be resolved.

29. **BeanNotOfRequiredTypeException**  
    Thrown when a bean is found but is not of the required type.

30. **PropertyVetoException**  
    Thrown when a property change is vetoed by a listener.

This list now covers general, collection-related, and bean-related exceptions, providing a comprehensive overview of common Java exceptions you may encounter during development.


## Runnable vs Callable

### Runnable vs Callable: Key Differences

| **Feature**              | **Runnable**                                  | **Callable**                                          |
|--------------------------|-----------------------------------------------|------------------------------------------------------|
| **Introduced in**         | Java 1.0                                      | Java 5 (as part of `java.util.concurrent`)            |
| **Return Type**           | `void` (no result returned)                   | Returns a result of type `V` through `Future<V>`      |
| **Method to Implement**   | `run()`                                       | `call()`                                              |
| **Exception Handling**    | Cannot throw checked exceptions               | Can throw checked exceptions                          |
| **Concurrency Framework** | Works with `Thread`, `Executor`, etc.         | Works with `ExecutorService`, `FutureTask`, etc.      |
| **Usage**                 | Suitable for simple tasks without results     | Suitable for tasks that return results or throw exceptions |
| **Concurrency**           | Can be executed by `Thread`, `ExecutorService`| Can be executed by `ExecutorService`, `Future`, etc.  |
| **Syntax**                | `Runnable task = () -> { ... };`              | `Callable<V> task = () -> { return V; };`            |

#### Example Runnable:
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class RunnableExample {
    public static void main(String[] args) {
        // Create a Runnable task
        Runnable task = () -> {
            System.out.println("Runnable Task is running...");
            try {
                Thread.sleep(2000);  // Simulate a long-running task
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Runnable Task completed.");
        };

        // Use ExecutorService to run the Runnable task
        ExecutorService executor = Executors.newSingleThreadExecutor();
        executor.execute(task);  // No result is returned, we just run the task

        // Shut down the executor
        executor.shutdown();
    }
}

```

#### Callable
```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.ExecutionException;

public class CallableExample {
    public static void main(String[] args) {
        // Create a Callable task
        Callable<Integer> task = () -> {
            System.out.println("Callable Task is running...");
            Thread.sleep(2000);  // Simulate a long-running task
            System.out.println("Callable Task completed.");
            return 42;  // Return a result
        };

        // Use ExecutorService to submit the Callable task
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> future = executor.submit(task);  // Get a Future to hold the result

        try {
            // Retrieve the result of the Callable task
            Integer result = future.get();  // Blocking call, waits for the task to complete
            System.out.println("Callable Task result: " + result);  // Prints 42
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            // Shut down the executor
            executor.shutdown();
        }
    }
}

```

## Future vs CompletableFuture

| Feature                  | Future                                      | CompletableFuture                                  |
|--------------------------|---------------------------------------------|---------------------------------------------------|
| **Asynchronous Handling** | Only allows blocking operations to retrieve the result using `get()`. | Provides non-blocking, asynchronous operations using callbacks (`thenApply`, `thenAccept`, etc.). |
| **Result Handling**       | Blocks until the result is available.       | Can be handled with callbacks, without blocking.   |
| **Chaining**              | No support for chaining dependent tasks.    | Supports method chaining for task pipelines.       |
| **Exception Handling**    | Must handle exceptions after the task completes using `get()`. | Allows exception handling using `exceptionally`, `handle`, or `whenComplete`. |
| **Completion Triggering** | Only completes when the task is done.       | Can manually complete using `complete()` or `completeExceptionally()`. |
| **Concurrency**           | Executes a single task.                     | Can combine multiple asynchronous tasks using `allOf()`, `anyOf()`, etc. |
| **Cancellation**          | Can be cancelled using `cancel()`.          | Can be cancelled but also provides a way to trigger a callback when cancelled. |
| **Parallel Execution**    | Not well-suited for parallel task execution. | Natively supports parallel execution with `supplyAsync()`. |


### Future
```java
import java.util.concurrent.*;

public class FutureExample {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        // Submit a task to the executor
        Future<String> future = executor.submit(() -> {
            Thread.sleep(2000);  // Simulating a long-running task
            return "Future Task Completed";
        });

        // Do some other work, then wait for the task to complete
        System.out.println("Doing other work...");
        
        // Blocking call to get the result
        String result = future.get();  
        System.out.println(result);

        // Shut down the executor
        executor.shutdown();
    }
}

```

### COmpletableFuture
```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureExample {
    public static void main(String[] args) {
        // Asynchronous task using CompletableFuture
        CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> {
            try {
                Thread.sleep(2000);  // Simulating a long-running task
            } catch (InterruptedException e) {
                throw new IllegalStateException(e);
            }
            return "CompletableFuture Task Completed";
        });

        // Attach a callback to handle the result
        completableFuture.thenAccept(result -> System.out.println(result));
        
        // Do some other work while the task is still running
        System.out.println("Doing other work...");

        // Keep the main thread alive until the CompletableFuture task completes
        completableFuture.join();  // Non-blocking waiting for completion
    }
}

```


## Important methods of CompletableFuture and ExecutorService

Here are the important methods for CompletableFuture and ExecutorService in Java's java.util.concurrent package:

CompletableFuture
complete(T value)

Completes the CompletableFuture with the given value.
completeExceptionally(Throwable ex)

Completes the CompletableFuture with an exception.
thenApply(Function<? super T,? extends U> fn)

Returns a new CompletableFuture that is completed by applying the given function to the result of this CompletableFuture.
thenAccept(Consumer<? super T> action)

Returns a new CompletableFuture that, when this CompletableFuture completes normally, will execute the given action with the result.
thenRun(Runnable action)

Returns a new CompletableFuture that, when this CompletableFuture completes normally, will execute the given action.
exceptionally(Function<Throwable, ? extends T> fn)

Returns a new CompletableFuture that is completed with the result of the given function if this CompletableFuture completed exceptionally.
allOf(CompletableFuture<?>... futures)

Returns a new CompletableFuture that is completed when all of the given CompletableFutures complete.
anyOf(CompletableFuture<?>... futures)

Returns a new CompletableFuture that is completed when any of the given CompletableFutures complete.
ExecutorService
submit(Callable<T> task)

Submits a Callable task for execution and returns a Future representing the pending results of the task.
submit(Runnable task)

Submits a Runnable task for execution and returns a Future representing the pending results of the task.
invokeAll(Collection<? extends Callable<T>> tasks)

Executes the given tasks, returning a list of Future objects.
invokeAny(Collection<? extends Callable<T>> tasks)

Executes the given tasks and returns the result of the first successfully completed task.
shutdown()

Initiates an orderly shutdown in which previously submitted tasks are executed but no new tasks will be accepted.
shutdownNow()

Attempts to stop all actively executing tasks and halts the processing of waiting tasks.
isShutdown()

Returns true if this executor has been shut down.
isTerminated()

Returns true if all tasks have completed following shut down.

