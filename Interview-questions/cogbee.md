## 1.Self-introduction&current project

Hi, my name is Ellie,I’m a software engineer with about 8 years of experience in IT. I specialize in designing and developing web applications using Java technologies. I've got a solid background in both backend and frontend development and I’m skilled with modern frameworks and tools like Spring Boot, Angular, and AWS. I'm passionate about building scalable and efficient systems, and I've successfully worked on many high-impact projects over the years.

Right now, I'm working at Chewy, an online retailer for pet products. My job is to improve their eCommerce platform to make it easier and more enjoyable for users.

The project I worked on now was developing a new ecommerce platform using Java, Spring Boot, and Angular. We set up a microservice architecture and I designed and deployed multiple microservices like product Service, order Service, notification Service.
We used PostgreSQL, MongoDB, and cassandra for different data needs and integrated Elasticsearch for better search features. We deployed everything on AWS using services like EC2, EKS, and RDS.

Now,this platform delivers faster and more relevant search results, ensures high availability, and can handle thousands of concurrent users. This has greatly improved the shopping experience for Chewy's customers and streamlined their operations.

(Optional):
Before Chewy, I worked on an online banking system for Citizens Bank, leading the development of microservices for user management, secure fund transfers, and payments. I've also worked on a CRM system for Meituan, an Inventory Tracking System for Unilever, and an After-Sales Service System for Bosch. Each project had its own challenges, but I always focused on delivering high-quality and scalable solutions.

## 2.Which data structure you used in your project and how to analyze time complexity

    **HashMap:**

    1.Purpose:
             We use HashMaps primarily for quick lookups and caching. This data structure is highly efficient for scenarios where we need to store key-value pairs and perform frequent retrievals.

    2.Time Complexity:

    Insertion (put): O(1) on average, since it involves computing the hash and placing the entry in the correct bucket.

    Retrieval (get): O(1) on average, as it involves computing the hash and locating the entry in the corresponding bucket.

    Deletion (remove): O(1) on average, similar to insertion and retrieval.

    Worst-Case Complexity: O(n) for all operations if all keys hash to the same bucket (highly unlikely with a good hash function).

    3.Usage in Projects:

        Caching: Storing frequently accessed data to improve retrieval times.

        Configuration Settings: Managing application configurations where quick access to settings is required.

        Counting Frequencies: Tracking occurrences of elements in data processing tasks.

## 3.Difference between Binary Tree and Binary Search Tree

    - A Binary Tree is a tree data structure in which each node has at most two children, referred to as the left child and the right child.
    - A Binary Search Tree (BST) is a type of Binary Tree where each node follows the property: the left subtree contains only nodes with keys less than the node’s key, and the right subtree contains only nodes with keys greater than the node’s key.

## 4.Time complexity for binary Tree and Binary Search Tree

- For a Binary Tree:
  Insertion: O(n)
  Deletion: O(n)
  Search: O(n)
- For a Binary Search Tree (assuming it's balanced):
  Insertion: O(log n)
  Deletion: O(log n)
  Search: O(log n)
  If the BST is unbalanced, these operations can degrade to O(n).

## 5.How to create a immutable Class

To create an immutable class, you typically follow these guidelines:

1. **Declare the class as `final`**: This prevents other classes from extending it, which could potentially add mutable behavior through subclassing.

2. **Make fields `private` and `final`**: This ensures that fields cannot be accessed or modified directly from outside the class and prevents them from being reassigned once initialized.

3. **Do not provide setter methods**: Since you want to prevent modification of the object's state after creation, do not provide any methods that modify the state of the object.

4. **Ensure mutable fields are deeply copied or made immutable**: If your class contains references to mutable objects (e.g., collections), ensure that those objects are either deeply copied during construction or encapsulated in a way that prevents external modification.

5. **Constructors for initialization**: Provide constructors or factory methods that initialize all the fields of the object. Once the object is initialized, its state remains constant.

6. **Avoid mutable return types**: If your class has methods that return references to mutable objects (like arrays or collections), make sure those objects are also immutable or are not shared externally.

### Example of Immutable Class

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

## 6.The advantage of the stream api.

Java Stream API is used to process collections of objects. A stream is a sequence of elements that can be processed in a functional style. Operations on a stream can be intermediate (map, filter) or terminal (forEach, collect).

- Concise and Readable Code: It allows for more readable and maintainable code by using operations like filter, map, and reduce.

- Functional Programming: Promotes a functional programming style with lambda expressions and method references.

- Parallel Processing: Simplifies parallel processing, making it easy to utilize multiple cores for better performance.

- Pipeline Operations: Supports chaining of multiple operations in a clear and concise flow.

- Lazy Evaluation: Operations are evaluated lazily, which can improve performance by executing only when necessary.

- Reduction Operations: Provides powerful reduction operations for aggregating or summarizing data efficiently.

- Type Safety: Ensures type-safe operations with generics, catching errors at compile time.

## 7.map() vs flatMap()

- **map**:

  - **Purpose**: Transforms each element in the stream into another object using a given function.
  - **Result**: Produces a stream of the same structure but with transformed elements.
  - **Example**: Converting a list of strings to their lengths.
    ```java
    List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
    List<Integer> lengths = names.stream()
                                 .map(String::length)
                                 .collect(Collectors.toList());
    ```

- **flatMap**:
  - **Purpose**: Transforms each element into a stream of objects, then flattens these streams into a single stream.
  - **Result**: Produces a single, flat stream from multiple nested streams.
  - **Example**: Flattening a list of lists into a single list.
    ```java
    List<List<String>> nestedList = Arrays.asList(
        Arrays.asList("a", "b"),
        Arrays.asList("c", "d")
    );
    List<String> flatList = nestedList.stream()
                                      .flatMap(Collection::stream)
                                      .collect(Collectors.toList());
    ```

## 8.Strategy to improve system performance

To improve system performance, I would focus on the following strategies:

1. **Optimize Database Queries and Use Indexing**:

   - **Explanation**: Ensure that queries are efficient and use indexes to speed up data retrieval. Indexes can significantly reduce the time taken for search operations by quickly locating the data.

2. **Implement Caching Strategies**:

   - **Explanation**: Cache frequently accessed data to reduce database load and access times. This can be done using in-memory caches like Redis or Memcached, which provide faster data retrieval.

3. **Use Asynchronous Processing**:

   - **Explanation**: Perform time-consuming operations asynchronously to prevent blocking and improve system responsiveness. This can be achieved with asynchronous APIs or background processing.

4. **Optimize Code and Data Structures**:

   - **Explanation**: Ensure the code is efficient and uses the most appropriate data structures for the task. This includes minimizing unnecessary computations and choosing data structures with optimal time complexity for operations.

5. **Use Load Balancing and Scaling Techniques**:
   - **Explanation**: Distribute incoming traffic across multiple servers using load balancers to avoid overloading a single server. Additionally, implement horizontal scaling to add more servers as demand increases, ensuring the system can handle higher loads.

## 9.Scenario use HashMap and TreeMap

- HashMap: When you need fast access and don’t care about the order of elements. Ideal for caching, where lookup time is critical.
- TreeMap: When you need to maintain a sorted order of elements. Useful in cases where ordered traversal of keys is required.

## 10.Algorithm in project

In our project, we used the **Quicksort** algorithm for sorting data due to its efficient average-case time complexity of O(n log n). Additionally, we implemented **Dijkstra's** algorithm for finding the shortest paths in a graph representing product recommendations.

## 11.What working with concurrency/multi-threading,how do you solve the issue.

**Issue:** **Deadlock**

In one of our projects, we encountered a **deadlock** issue. Deadlock occurs when two or more threads are blocked forever, waiting for each other to release resources. This happens when multiple threads acquire locks on resources in different orders, leading to a cycle of dependencies that prevent progress.

### Example Scenario:

Two threads were trying to acquire two locks in different orders. Thread A held Lock 1 and was waiting to acquire Lock 2, while Thread B held Lock 2 and was waiting to acquire Lock 1. This created a deadlock situation.

### Solution:

1. **Lock Ordering:**

   - We established a global ordering for all locks and enforced that all threads acquire locks in this predefined order. This eliminated the possibility of circular dependencies and prevented deadlocks.

   ```java
   public class ResourceManager {
       private final Object lock1 = new Object();
       private final Object lock2 = new Object();

       public void process() {
           synchronized (lock1) {
               // Work with lock1
               synchronized (lock2) {
                   // Work with lock2
               }
           }
       }
   }
   ```

2. **Timeouts:**

   - We used timeouts when trying to acquire locks, which allowed threads to fail gracefully if a lock could not be acquired within a specified time. This helped prevent threads from waiting indefinitely.

   ```java
   boolean acquired = false;
   try {
       acquired = lock.tryLock(10, TimeUnit.SECONDS);
       if (acquired) {
           // Perform critical section work
       }
   } catch (InterruptedException e) {
       Thread.currentThread().interrupt();
   } finally {
       if (acquired) {
           lock.unlock();
       }
   }
   ```

3. **Deadlock Detection:**

   - We implemented deadlock detection algorithms to identify and resolve deadlocks if they occurred. This involved periodically checking for cycles in the resource allocation graph and taking corrective actions.

4. **Resource Hierarchies:**

   - We refactored the code to minimize the number of locks and resource contention by using higher-level abstractions and better design patterns. This reduced the chances of deadlocks occurring.

5. **Testing and Simulation:**
   - We created scenarios to simulate potential deadlocks and tested the system under concurrent conditions to identify and fix deadlocks before deploying to production.

## 12.Difference between the ArrayList and LinkedList.

- ArrayList:
  - Uses a dynamic array to store elements.
  - Provides O(1) time complexity for random access and O(n) for adding/removing elements at the beginning/middle.
- LinkedList:
  - Uses a doubly linked list to store elements.
  - Provides O(1) time complexity for adding/removing elements at the beginning/middle but O(n) for random access.

## 13.How can we connect more database in the single spring project.

To connect multiple databases in a single Spring project, follow these steps:

1. **Define Multiple Data Sources:**

   - Configure separate `DataSource` beans for each database, specifying their respective connection properties.

   ```java
   @Bean
   @ConfigurationProperties(prefix = "spring.datasource.db1")
   public DataSource dataSource1() {
       return DataSourceBuilder.create().build();
   }

   @Bean
   @ConfigurationProperties(prefix = "spring.datasource.db2")
   public DataSource dataSource2() {
       return DataSourceBuilder.create().build();
   }
   ```

2. **Set Up Multiple `EntityManagerFactory` Beans:**

   - Create `EntityManagerFactory` beans for each data source, specifying different packages for entity scanning.

   ```java
   @Bean
   @Primary
   public LocalContainerEntityManagerFactoryBean entityManagerFactory1(EntityManagerFactoryBuilder builder,
                                                                         @Qualifier("dataSource1") DataSource dataSource) {
       return builder
           .dataSource(dataSource)
           .packages("com.example.model.db1")
           .persistenceUnit("db1")
           .build();
   }

   @Bean
   public LocalContainerEntityManagerFactoryBean entityManagerFactory2(EntityManagerFactoryBuilder builder,
                                                                         @Qualifier("dataSource2") DataSource dataSource) {
       return builder
           .dataSource(dataSource)
           .packages("com.example.model.db2")
           .persistenceUnit("db2")
           .build();
   }
   ```

3. **Configure Transaction Managers:**

   - Define transaction managers for each `EntityManagerFactory`.

   ```java
   @Bean
   @Primary
   public PlatformTransactionManager transactionManager1(@Qualifier("entityManagerFactory1") EntityManagerFactory emf) {
       return new JpaTransactionManager(emf);
   }

   @Bean
   public PlatformTransactionManager transactionManager2(@Qualifier("entityManagerFactory2") EntityManagerFactory emf) {
       return new JpaTransactionManager(emf);
   }
   ```

4. **Configure Repository Scanning:**

   - Use `@EnableJpaRepositories` to specify which repositories are associated with each `EntityManagerFactory` and transaction manager.

   ```java
   @EnableJpaRepositories(
       basePackages = "com.example.repository.db1",
       entityManagerFactoryRef = "entityManagerFactory1",
       transactionManagerRef = "transactionManager1"
   )
   public class Db1Config {
   }

   @EnableJpaRepositories(
       basePackages = "com.example.repository.db2",
       entityManagerFactoryRef = "entityManagerFactory2",
       transactionManagerRef = "transactionManager2"
   )
   public class Db2Config {
   }
   ```

## 14.Use the interceptor?

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

## 15.Coding

- Employee: id,name,date,gender,departmentName,joinDate
  - Use stream api
  - Give the employee account who
  - From IT department
  - Age between 45 and 55
  - In this company more than 10 years.

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
