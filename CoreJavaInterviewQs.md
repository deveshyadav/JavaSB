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
