### Introduction & Current Project

**Self-introduction:**

Hi, my name is Ellie. I’m a software engineer with about 8 years of experience in IT. I specialize in designing and developing web applications using Java technologies. I've got a solid background in both backend and frontend development and I’m skilled with modern frameworks and tools like Spring Boot, Angular, and AWS. I'm passionate about building scalable and efficient systems, and I've successfully worked on many high-impact projects over the years.

Right now, I'm working at Chewy, an online retailer for pet products. My job is to improve their eCommerce platform to make it easier and more enjoyable for users.

The project I worked on now was developing a new eCommerce platform using Java, Spring Boot, and Angular. We set up a microservice architecture and I designed and deployed multiple microservices like Product Service, Order Service, and Notification Service. We used PostgreSQL, MongoDB, and Cassandra for different data needs and integrated Elasticsearch for better search features. We deployed everything on AWS using services like EC2, EKS, and RDS.

Now, this platform delivers faster and more relevant search results, ensures high availability, and can handle thousands of concurrent users. This has greatly improved the shopping experience for Chewy's customers and streamlined their operations.

Before Chewy, I worked on an online banking system for Citizens Bank, leading the development of microservices for user management, secure fund transfers, and payments. I've also worked on a CRM system for Meituan, an Inventory Tracking System for Unilever, and an After-Sales Service System for Bosch. Each project had its own challenges, but I always focused on delivering high-quality and scalable solutions.

---

### Data Structures

**Which data structure you used in your project and how to analyze time complexity**

**HashMap:**

**Purpose:**
We use HashMaps primarily for quick lookups and caching. This data structure is highly efficient for scenarios where we need to store key-value pairs and perform frequent retrievals.

**Time Complexity:**

- Insertion (put): O(1) on average, since it involves computing the hash and placing the entry in the correct bucket.
- Retrieval (get): O(1) on average, as it involves computing the hash and locating the entry in the corresponding bucket.
- Deletion (remove): O(1) on average, similar to insertion and retrieval.
- Worst-Case Complexity: O(n) for all operations if all keys hash to the same bucket (highly unlikely with a good hash function).

**Usage in Projects:**

- Caching: Storing frequently accessed data to improve retrieval times.
- Configuration Settings: Managing application configurations where quick access to settings is required.
- Counting Frequencies: Tracking occurrences of elements in data processing tasks.

**Explanation:**
HashMap is a highly efficient data structure for scenarios where quick access to data is critical. It leverages hashing to distribute entries across buckets, providing average-case constant time complexity for basic operations.

---

**Difference between Binary Tree and Binary Search Tree**

**Explanation:**

- **Binary Tree:**

  - General tree structure where each node has at most two children, referred to as the left child and the right child.
  - No specific ordering of elements.

- **Binary Search Tree (BST):**
  - A type of Binary Tree where each node follows the property: the left subtree contains only nodes with keys less than the node’s key, and the right subtree contains only nodes with keys greater than the node’s key.
  - Allows efficient searching, insertion, and deletion operations due to this ordering property.

**Time Complexity for Binary Tree and Binary Search Tree:**

- **Binary Tree:**
  - Insertion: O(n)
  - Deletion: O(n)
  - Search: O(n)
- **Binary Search Tree (assuming it's balanced):**
  - Insertion: O(log n)
  - Deletion: O(log n)
  - Search: O(log n)
  - If the BST is unbalanced, these operations can degrade to O(n).

**Explanation:**
Binary Search Trees provide more efficient operations compared to general Binary Trees due to the ordering of elements, which allows operations to be performed in logarithmic time on average.

---

**Collision resolution in Hashing:**

**Explanation:**

- **Chaining:** Use linked lists to store multiple values that hash to the same bucket.
- **Open Addressing:** Find another slot within the hash table (linear probing, quadratic probing, double hashing).

**Usage in Projects:**
Efficiently manage collisions in HashMap to maintain performance.

---

**How does HashMap work and is implemented in Java?**

**Explanation:**

- **HashMap** stores key-value pairs in an array of buckets.
- The key’s hash code determines the bucket.
- Collisions are resolved using chaining (linked lists) or tree structures.
- On reaching a threshold, the map resizes by doubling its capacity and rehashing entries.

**Usage in Projects:**
Used for efficient key-value storage and retrieval, such as caching frequently accessed data.

---

**Difference between ArrayList and LinkedList**

**Explanation:**

- **ArrayList:**

  - Implements a resizable array.
  - Faster random access (O(1)).
  - Slower insertions and deletions (O(n)) due to shifting elements.
  - Better for read-intensive operations.

- **LinkedList:**
  - Implements a doubly-linked list.
  - Slower random access (O(n)).
  - Faster insertions and deletions (O(1)) when manipulating at the ends or known positions.
  - Better for write-intensive operations.

**Usage in Projects:**
Choose based on the need for fast access (ArrayList) vs. fast modification (LinkedList).

---

**Difference between TreeMap and HashMap**

**Explanation:**

- **TreeMap:**

  - Implements a Red-Black tree.
  - Sorted order of keys.
  - O(log n) time complexity for get, put, remove operations.

- **HashMap:**
  - Uses a hash table.
  - No order guarantee.
  - O(1) average time complexity for get, put, remove operations, but can degrade to O(n) in worst-case scenarios.

**Usage in Projects:**
Use TreeMap when sorted order is needed; use HashMap for quick access without order.

---

**Fail-fast and fail-safe iterator**

**Explanation:**

- **Fail-fast:** Throws `ConcurrentModificationException` if the collection is modified while iterating (e.g., `ArrayList`, `HashMap`).
- **Fail-safe:** Does not throw an exception if the collection is modified while iterating (e.g., `ConcurrentHashMap`, `CopyOnWriteArrayList`).

**Usage in Projects:**
Choose based on the need for concurrent modifications.

---

### Java and Concurrency

**Different ways of creating threads in Java:**

**Explanation:**

- Extend `Thread` class and override `run()` method.
- Implement `Runnable` interface and pass an instance to `Thread` constructor.
- Implement `Callable` interface for tasks that return a result and use `ExecutorService`.

**Usage in Projects:**
Use appropriate method based on the task's complexity and return type requirements.

---

**What is deadlock, and how to avoid it?**

**Explanation:**

- **Deadlock:** Occurs when two or more threads are blocked forever, waiting for each other.
- **Avoidance:**
  - Using a lock hierarchy.
  - Acquiring all locks at once.
  - Using timeout for lock attempts.
  - Detecting deadlock with a resource allocation graph.

**Usage in Projects:**
Design thread interactions to prevent deadlocks, ensuring smooth concurrent execution.

---

**How do you handle concurrent modification in Java?**

**Explanation:**

- Use concurrent collections (`ConcurrentHashMap`, `CopyOnWriteArrayList`).
- Use synchronization or locks.
- Avoid modifying collections while iterating or use fail-safe iterators.

**Usage in Projects:**
Ensure thread-safe operations on collections to avoid `ConcurrentModificationException`.

---

**How can we make a singleton in Java?**

**Explanation:**

- Use a private constructor and a static instance.
- Use double-checked locking or `Bill Pugh Singleton Design`.
- Use `enum` for a thread-safe and serializable singleton.

**Usage in Projects:**
Guarantee a single instance of a class, such as a configuration manager or logger.

---

**What will happen if we do not have a synchronized method for returning a singleton instance in a multi-threaded environment?**

**Explanation:**
Multiple threads could create multiple instances of the singleton class, violating the singleton principle.

**Usage in Projects:**
Ensure thread-safe singleton creation to maintain a single instance.

---

**When working with concurrency, we have some issues, can you tell me which concurrency and how do you solve the issue?**

**Explanation:**

- Common concurrency issues include race conditions, deadlocks, and thread starvation.
- **Solutions:**
  - **Race conditions:** Use synchronized blocks, locks (e.g., `ReentrantLock`), or atomic variables.
  - **Deadlocks:** Avoid nested locks, use timeout locks (e.g., `tryLock()`), and deadlock detection tools.
  - **Thread starvation:** Ensure fair scheduling policies, use thread pools, and prioritize threads appropriately.

**Usage in Projects:**
Implement concurrency control measures to ensure reliable multi-threaded operations.

---

### Spring and Spring Boot

**How do you configure caching in a Spring Boot application?**

**Explanation:**

- Add the necessary dependencies (`spring-boot-starter-cache`).
- Enable caching by adding `@EnableCaching` to a configuration class.
- Configure a cache manager (e.g., `ConcurrentMapCacheManager`, `EhCacheCacheManager`).
- Use caching annotations such as `@Cacheable`, `@Cache

Put`, and `@CacheEvict` on methods.

**Usage in Projects:**
Improve application performance by caching frequently accessed data.

---

**What are Spring Boot profiles?**

**Explanation:**

- Profiles provide a way to segregate parts of your application configuration and make it available only in certain environments. For example, you can have different configurations for development, testing, and production environments.
- Use `@Profile` annotation to indicate that a component is only available in a specific profile.
- Activate a profile using `spring.profiles.active` property in `application.properties` or via command line arguments.

**Usage in Projects:**
Manage different configurations for different environments easily.

---

**How do you use Spring Boot interceptor?**

**Explanation:**

- Create a class that implements `HandlerInterceptor`.
- Override methods like `preHandle()`, `postHandle()`, and `afterCompletion()`.
- Register the interceptor with a `WebMvcConfigurer` implementation by overriding the `addInterceptors()` method.

**Usage in Projects:**
Implement cross-cutting concerns like logging, authentication, and rate limiting.

---

**How to handle external configuration in Spring Boot**

**Explanation:**

- Use `application.properties` or `application.yml`.
- Use `@Value` annotation or `Environment` object to inject configuration properties.
- Use `@ConfigurationProperties` for structured configuration.

**Usage in Projects:**
Manage external configuration for flexibility and maintainability.

---

**How do you handle authentication and authorization in Spring Boot?**

**Explanation:**

- Use Spring Security to handle authentication and authorization.
- Configure security settings in a class extending `WebSecurityConfigurerAdapter`.
- Use `@EnableWebSecurity` and `@Configuration` annotations.
- Implement custom `UserDetailsService` and `PasswordEncoder`.
- Define roles and permissions using `@PreAuthorize` and `@Secured` annotations.

**Usage in Projects:**
Secure applications by implementing robust authentication and authorization mechanisms.

---

**How can you secure a Spring Boot application in Spring Boot Security**

**Explanation:**

- Use Spring Security to secure the application.
- Configure security settings in a class extending `WebSecurityConfigurerAdapter`.
- Implement user authentication and authorization.
- Use OAuth2, JWT, or Basic Authentication.

**Usage in Projects:**
Ensure secure access to application resources.

---

**How can we connect more databases in a single Spring project?**

**Explanation:**

- Define multiple `DataSource` beans.
- Use `@Primary` to specify the default data source.
- Configure `EntityManagerFactory` and `TransactionManager` for each data source.
- Use `@EnableJpaRepositories` with the `entityManagerFactoryRef` and `transactionManagerRef` attributes.

**Usage in Projects:**
Manage connections to multiple databases for various data needs.

---

### Microservices and Design Patterns

**In microservices, what is an API gateway?**

**Explanation:**

- An API gateway is a server that acts as an API front-end, handling requests from clients, routing them to appropriate microservices, and aggregating responses.
- It provides functionalities like authentication, logging, rate limiting, and load balancing.

**Usage in Projects:**
Simplify client interactions with microservices and handle cross-cutting concerns.

---

**How do you ensure that the microservices are scalable and resilient?**

**Explanation:**

- Use containerization (e.g., Docker) and orchestration (e.g., Kubernetes).
- Implement load balancing.
- Use circuit breakers, retries, and timeouts for resilience.
- Monitor and auto-scale based on demand.

**Usage in Projects:**
Design microservices to handle varying loads and recover from failures gracefully.

---

**What is the recommended approach for two microservices needing to update the same database?**

**Explanation:**

- Use distributed transactions (e.g., two-phase commit) or compensating transactions.
- Prefer eventual consistency and design the system to handle inconsistencies.

**Usage in Projects:**
Ensure data integrity and consistency in microservices architecture.

---

**How do you handle load balancing in a microservices environment to ensure optimal performance and resource utilization?**

**Explanation:**

- Use a load balancer (e.g., Nginx, HAProxy).
- Use service discovery and client-side load balancing (e.g., Netflix Ribbon, Spring Cloud LoadBalancer).
- Distribute requests evenly across instances to ensure no single instance is overwhelmed.

**Usage in Projects:**
Optimize resource utilization and performance in microservices.

---

**What is the circuit breaker pattern?**

**Explanation:**

- The circuit breaker pattern is a design pattern used to detect failures and encapsulate the logic of preventing a failure from constantly recurring during maintenance, temporary external system failure, or unexpected system difficulties.
- It prevents an application from trying to perform an operation that's likely to fail.
- Use libraries like Netflix Hystrix or Resilience4j to implement this pattern.

**Usage in Projects:**
Enhance the resilience of microservices by preventing cascading failures.

---

**What is the builder design pattern?**

**Explanation:**

- The builder design pattern is used to construct a complex object step by step.
- It provides a way to construct a complex object by specifying its type and content, while hiding the internal representation or construction process.

**Usage in Projects:**
Create complex objects in a readable and maintainable way.

---

**What is the factory design pattern?**

**Explanation:**

- The factory design pattern provides an interface for creating objects without specifying the exact class to instantiate.
- It delegates the responsibility of object instantiation to subclasses or a separate method.

**Usage in Projects:**
Encapsulate object creation logic to increase flexibility and reuse.

---

**What is the adapter design pattern?**

**Explanation:**

- The adapter pattern allows incompatible interfaces to work together.
- It acts as a bridge between two incompatible interfaces by wrapping an object with an adapter.

**Usage in Projects:**
Enable integration between systems with incompatible interfaces.

---

### Java Features and Concepts

**What is Metaspace?**

**Explanation:**

- Metaspace is a memory space in Java introduced in JDK 8 that replaces the PermGen (Permanent Generation) space. It stores class metadata. Unlike PermGen, Metaspace is not part of the Java heap and can grow dynamically, reducing the risk of `OutOfMemoryError`.

**Usage in Projects:**
Manage class metadata efficiently without risking memory errors.

---

**Why do we need Metaspace since we already have PermGen?**

**Explanation:**

- Metaspace was introduced to overcome limitations and problems associated with PermGen, such as fixed size leading to `OutOfMemoryError`. Metaspace dynamically resizes, improving memory management and eliminating the need for manual configuration.

**Usage in Projects:**
Benefit from improved memory management and flexibility.

---

**What are compile-time polymorphism and run-time polymorphism?**

**Explanation:**

- **Compile-time polymorphism** (or static polymorphism) is method overloading, where multiple methods have the same name but different parameters.
- **Run-time polymorphism** (or dynamic polymorphism) is method overriding, where a subclass provides a specific implementation for a method declared in a parent class.

**Usage in Projects:**
Implement flexible and extensible code through method overloading and overriding.

---

**What is the SOLID principle?**

**Explanation:**

- SOLID is an acronym for five design principles that help software developers design maintainable and extendable classes:
  - **S**ingle Responsibility Principle: A class should have only one reason to change.
  - **O**pen/Closed Principle: Classes should be open for extension but closed for modification.
  - **L**iskov Substitution Principle: Subtypes must be substitutable for their base types.
  - **I**nterface Segregation Principle: No client should be forced to depend on methods it does not use.
  - **D**ependency Inversion Principle: High-level modules should not depend on low-level modules but on abstractions.

**Usage in Projects:**
Design robust and maintainable software by adhering to SOLID principles.

---

**What is CompletableFuture?**

**Explanation:**

- `CompletableFuture` is a class in Java that represents a future result of an asynchronous computation. It allows you to explicitly complete it and attach a callback to be executed upon completion.

**Usage in Projects:**
Implement asynchronous programming for better performance and responsiveness.

---

**How to create an immutable class**

**Explanation:**
To create an immutable class, follow these guidelines:

1. **Declare the class as `final`:** This prevents other classes from extending it.
2. **Make fields `private` and `final`:** Ensures fields cannot be accessed or modified directly and cannot be reassigned once initialized.
3. **Do not provide setter methods:** Prevents modification of the object's state after creation.
4. **Ensure mutable fields are deeply copied or made immutable:** Protects the integrity of the object by preventing external modification.
5. **Constructors for initialization:** Provide constructors or factory methods to initialize all fields.
6. **Avoid mutable return types:** Return immutable objects or unmodifiable views.

**Example of Immutable Class:**

```java
import java.util.Collections;
import java.util.List;

public final class ImmutablePerson {
    private final String name;
    private final int age;
    private final List<String> hobbies;

    public ImmutablePerson(String name, int age, List<String> hobbies) {
        this.name = name;
        this.age = age;
        // Create a defensive copy of the list or use an unmodifiable list to ensure immutability
        this.hobbies = Collections.unmodifiableList(hobbies);
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public List<String> getHobbies() {
        return hobbies;  // Returns an unmodifiable view of the hobbies list
    }
}
```

**Usage in Projects:**
Ensure the integrity and thread-safety of

instances by making them immutable.

---

**What is the concept of overloading and overriding**

**Explanation:**

- **Overloading:** Multiple methods with the same name but different parameters within the same class.
- **Overriding:** A subclass provides a specific implementation for a method already defined in its superclass.

**Usage in Projects:**
Enhance code flexibility and reusability through method overloading and overriding.

---

**Scope of the protected keyword**

**Explanation:**

- The `protected` keyword allows access to the member variables and methods within the same package and subclasses in different packages.

**Usage in Projects:**
Control access to class members for better encapsulation and inheritance.

---

**Shallow copy and deep copy**

**Explanation:**

- **Shallow copy:** Copies the object's structure but not the objects it references.
- **Deep copy:** Copies the object and all objects it references.

**Usage in Projects:**
Choose based on the need to copy complex object graphs.

---

**OOP in Java?**

**Explanation:**
OOP (Object-Oriented Programming) principles include:

- **Encapsulation:** Hiding internal state and requiring all interaction to be performed through an object's methods.
- **Inheritance:** Defining new classes based on existing classes.
- **Polymorphism:** Allowing entities to be treated as instances of their parent class rather than their actual class.
- **Abstraction:** Hiding the implementation details and exposing only the functionality.

**Usage in Projects:**
Design software using OOP principles for better organization, maintainability, and scalability.

---

### Stream API and Functional Programming

**The advantage of the stream API**

**Explanation:**
Java Stream API is used to process collections of objects. A stream is a sequence of elements that can be processed in a functional style. Operations on a stream can be intermediate (map, filter) or terminal (forEach, collect).

**Advantages:**

- **Concise and Readable Code:** It allows for more readable and maintainable code by using operations like filter, map, and reduce.
- **Functional Programming:** Promotes a functional programming style with lambda expressions and method references.
- **Parallel Processing:** Simplifies parallel processing, making it easy to utilize multiple cores for better performance.
- **Pipeline Operations:** Supports chaining of multiple operations in a clear and concise flow.
- **Lazy Evaluation:** Operations are evaluated lazily, which can improve performance by executing only when necessary.
- **Reduction Operations:** Provides powerful reduction operations for aggregating or summarizing data efficiently.
- **Type Safety:** Ensures type-safe operations with generics, catching errors at compile time.

**Usage in Projects:**
Simplify data processing and improve code readability and performance.

---

**map() vs flatMap()**

**Explanation:**

- **map:**

  - **Purpose:** Transforms each element in the stream into another object using a given function.
  - **Result:** Produces a stream of the same structure but with transformed elements.
  - **Example:** Converting a list of strings to their lengths.
    ```java
    List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
    List<Integer> lengths = names.stream()
                                 .map(String::length)
                                 .collect(Collectors.toList());
    ```

- **flatMap:**
  - **Purpose:** Transforms each element into a stream of objects, then flattens these streams into a single stream.
  - **Result:** Produces a single, flat stream from multiple nested streams.
  - **Example:** Flattening a list of lists into a single list.
    ```java
    List<List<String>> nestedList = Arrays.asList(
        Arrays.asList("a", "b"),
        Arrays.asList("c", "d")
    );
    List<String> flatList = nestedList.stream()
                                      .flatMap(Collection::stream)
                                      .collect(Collectors.toList());
    ```

**Usage in Projects:**
Use `map` for one-to-one transformations and `flatMap` for one-to-many transformations.

---

### Performance and Optimization

**Strategy to improve system performance**

**Explanation:**
To improve system performance, focus on the following strategies:

1. **Optimize Database Queries and Use Indexing:**

   - Ensure that queries are efficient and use indexes to speed up data retrieval. Indexes can significantly reduce the time taken for search operations by quickly locating the data.

2. **Implement Caching Strategies:**

   - Cache frequently accessed data to reduce database load and access times. This can be done using in-memory caches like Redis or Memcached, which provide faster data retrieval.

3. **Use Asynchronous Processing:**

   - Perform time-consuming operations asynchronously to prevent blocking and improve system responsiveness. This can be achieved with asynchronous APIs or background processing.

4. **Optimize Code and Data Structures:**

   - Ensure the code is efficient and uses the most appropriate data structures for the task. This includes minimizing unnecessary computations and choosing data structures with optimal time complexity for operations.

5. **Use Load Balancing and Scaling Techniques:**
   - Distribute incoming traffic across multiple servers using load balancers to avoid overloading a single server. Additionally, implement horizontal scaling to add more servers as demand increases, ensuring the system can handle higher loads.

**Usage in Projects:**
Implement these strategies to enhance the performance, scalability, and responsiveness of the system.

---

### Miscellaneous

**Can you tell me the scenarios where you would use encapsulation in Java?**

**Explanation:**
Encapsulation is used to protect the state of an object by making its fields private and providing public getter and setter methods. Scenarios include:

- Ensuring data integrity by validating input in setter methods.
- Hiding the internal implementation details from the outside world.
- Making a class easier to maintain and understand by controlling how its data is accessed and modified.

**Usage in Projects:**
Ensure robust class design by encapsulating state and behavior.

---

**Can you tell me the scenarios where you would use inheritance in Java?**

**Explanation:**
Inheritance is used to create a new class based on an existing class. Scenarios include:

- Reusing code by inheriting properties and behaviors from a parent class.
- Establishing a hierarchical relationship between classes, such as creating specialized subclasses from a general superclass (e.g., `Animal` -> `Dog`, `Cat`).

**Usage in Projects:**
Leverage inheritance to promote code reuse and establish class hierarchies.

---

**Can you tell me the scenarios where you would use polymorphism in Java?**

**Explanation:**
Polymorphism allows objects to be treated as instances of their parent class rather than their actual class. Scenarios include:

- Implementing method overriding to provide different behaviors for subclasses.
- Using interfaces to enable multiple implementations of the same method (e.g., different sorting algorithms).

**Usage in Projects:**
Implement flexible and extensible code through polymorphism.

---

**Can you tell me the scenarios where you would use Optional class?**

**Explanation:**
`Optional` is used to handle null values and avoid `NullPointerException`. Scenarios include:

- Returning `Optional` from methods to indicate that the result may be absent.
- Using `Optional` to chain methods and avoid explicit null checks.

**Usage in Projects:**
Improve code safety and readability by using `Optional` to handle potential null values.

---

**Can you tell me the scenarios where you would use Functional Interface?**

**Explanation:**
Functional interfaces are used to implement functional programming concepts. Scenarios include:

- Passing behavior as an argument to methods (e.g., using lambda expressions).
- Implementing callbacks or event handlers.

**Usage in Projects:**
Leverage functional interfaces for concise and expressive code.

---

**Can you tell me the difference between some pre-defined Function Interfaces in Java? For example, Predicate, Consumer, etc.**

**Explanation:**

- **Predicate<T>:** Represents a boolean-valued function that takes one argument (`test()` method).
- **Consumer<T>:** Represents an operation that takes a single argument and returns no result (`accept()` method).
- **Function<T, R>:** Represents a function that takes one argument and produces a result (`apply()` method).
- **Supplier<T>:** Represents a supplier of results (`get()` method).

**Usage in Projects:**
Use appropriate functional interfaces to implement functional programming patterns.

---

**Can you tell me the scenarios where you would use Method Reference?**

**Explanation:**
Method references are used to make the code more readable and concise. Scenarios include:

- Reusing existing methods in lambda expressions.
- Referring to static methods, instance methods, or constructors.

**Usage in Projects:**
Simplify code by using method references where applicable.

---

**Can you tell me the difference between parallel streaming and sequential streaming?**

**Explanation:**

- **Sequential Stream:** Processes elements in a single thread.
- **Parallel Stream:** Splits the stream into multiple substreams and processes them in parallel using the ForkJoinPool, which can improve performance for large data sets.

**Usage in Projects:**
Choose parallel streams for large data sets to leverage multi-core processors.

---

**Coding: write a sorting algorithm (sort an integer array) by yourself, don't use any built-in sorting methods.**

**Example:**

```java
public class SortingExample {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j + 1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {64, 34,

25, 12, 22, 11, 90};
        bubbleSort(arr);
        System.out.println("Sorted array:");
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

**Explanation:**
Implementing a sorting algorithm like bubble sort helps in understanding basic algorithm concepts and improving problem-solving skills.

---

### SQL and Database Management

**Do you have experience in SQL databases?**

**Explanation:**
This will depend on your actual experience. For example, "Yes, I have experience working with SQL databases such as MySQL and PostgreSQL. I have designed schemas, written complex queries, and optimized database performance."

**Usage in Projects:**
Manage and manipulate data efficiently using SQL databases.

---

**Why do we need to use an index in a database?**

**Explanation:**
Indexes improve the speed of data retrieval operations on a database table at the cost of additional writes and storage space. They enable quick lookups and efficient query execution by reducing the amount of data that needs to be scanned.

**Usage in Projects:**
Enhance database performance by using indexes appropriately.

---

**Scenario use HashMap and TreeMap**

**Explanation:**

- **HashMap:** When you need fast access and don’t care about the order of elements. Ideal for caching, where lookup time is critical.
- **TreeMap:** When you need to maintain a sorted order of elements. Useful in cases where ordered traversal of keys is required.

**Usage in Projects:**
Choose based on the requirement for order (TreeMap) vs. speed (HashMap).

---

### Custom Algorithm

**Algorithm in project**

**Explanation:**
In our project, we used the **Quicksort** algorithm for sorting data due to its efficient average-case time complexity of O(n log n). Additionally, we implemented **Dijkstra's** algorithm for finding the shortest paths in a graph representing product recommendations.

**Usage in Projects:**
Implement efficient algorithms for sorting and pathfinding to optimize performance.

---

**Use the interceptor?**

**Explanation:**
**eCommerce System:**
In an eCommerce system, interceptors can be used for various purposes like logging, authentication, and request validation.

1. **Logging Requests and Responses:**

   - Implement an interceptor to log details about incoming requests and outgoing responses for monitoring and debugging.

   ```java
   @Component
   public class LoggingInterceptor implements HandlerInterceptor {

       @Override
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           // Log request details
           System.out.println("Incoming request: " + request.getRequestURI());
           return true;
       }

       @Override
       public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
           // Log response details
           System.out.println("Response status: " + response.getStatus());
       }
   }
   ```

2. **Rate Limiting:**

   - Implement an interceptor to enforce rate limits on API calls to prevent abuse and ensure fair usage.

   ```java
   @Component
   public class RateLimitingInterceptor implements HandlerInterceptor {

       private final RateLimiter rateLimiter = RateLimiter.create(100); // 100 requests per second

       @Override
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           if (rateLimiter.tryAcquire()) {
               return true;
           } else {
               response.setStatus(HttpServletResponse.SC_TOO_MANY_REQUESTS);
               return false;
           }
       }
   }
   ```

**Banking System:**
In a banking system, interceptors are crucial for security, transaction management, and auditing.

1. **Authentication and Authorization:**

   - Use an interceptor to verify user authentication and authorization before allowing access to sensitive operations.

   ```java
   @Component
   public class SecurityInterceptor implements HandlerInterceptor {

       @Override
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           String token = request.getHeader("Authorization");
           if (isValidToken(token)) {
               return true;
           } else {
               response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
               return false;
           }
       }

       private boolean isValidToken(String token) {
           // Validate token
           return true; // Example validation
       }
   }
   ```

2. **Transaction Logging:**

   - Implement an interceptor to log details of financial transactions for auditing and compliance purposes.

   ```java
   @Component
   public class TransactionLoggingInterceptor implements HandlerInterceptor {

       @Override
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           // Start transaction logging
           System.out.println("Transaction started: " + request.getRequestURI());
           return true;
       }

       @Override
       public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
           // End transaction logging
           System.out.println("Transaction completed: " + request.getRequestURI());
       }
   }
   ```

**Usage in Projects:**
Implement cross-cutting concerns using interceptors for better maintainability and scalability.

---

### Specific Coding Task

**Employee Filtering Example**

**Explanation:**
Filter employees based on specific criteria using Java Streams.

**Example:**

```java
import java.time.LocalDate;
import java.time.Period;
import java.util.List;
import java.util.stream.Collectors;

public class Employee {
    private int id;
    private String name;
    private LocalDate dateOfBirth;
    private String gender;
    private String departmentName;
    private LocalDate joinDate;

    // Constructors, getters and setters

    public static List<Employee> filterEmployees(List<Employee> employees) {
        return employees.stream()
                .filter(e -> "IT".equals(e.getDepartmentName()))
                .filter(e -> {
                    int age = Period.between(e.getDateOfBirth(), LocalDate.now()).getYears();
                    return age >= 45 && age <= 55;
                })
                .filter(e -> Period.between(e.getJoinDate(), LocalDate.now()).getYears() > 10)
                .collect(Collectors.toList());
    }
}
```

**Usage in Projects:**
Use streams to efficiently filter and process collections based on complex criteria.

---

This reorganization covers all the provided questions, removing duplicates and providing detailed explanations along with example code where applicable. This should help you prepare comprehensively for your interview.
