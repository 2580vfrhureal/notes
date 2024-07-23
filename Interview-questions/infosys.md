### Core Concept in Java: Object-Oriented Programming (OOP)

Java is a strongly object-oriented programming language, which means it heavily relies on concepts like classes, objects, inheritance, polymorphism, encapsulation, and abstraction.

### ConcurrentModificationException

This exception occurs when a collection is modified while it is being iterated over, typically using iterators. For example:

```java
List<String> list = new ArrayList<>(Arrays.asList("a", "b", "c"));
for (String s : list) {
    if (s.equals("b")) {
        list.remove(s); // This will throw ConcurrentModificationException
    }
}
```

### ClassCastException

This exception is thrown when an object is cast to a type that it is not an instance of. For example:

```java
Object x = new Integer(0);
String s = (String) x; // This will throw ClassCastException
```

### How HashMap Works Internally

HashMap in Java uses an array of buckets where each bucket is a linked list. When you add a key-value pair, a hash code is generated from the key, and the hash code determines the bucket where the entry will be stored. If two keys have the same hash code, they are stored in the same bucket but as separate nodes in the linked list.

### Adding Null Key to HashMap

HashMap allows one null key. The null key is always stored in the first bucket.

```java
Map<String, String> map = new HashMap<>();
map.put(null, "value");
```

### Comparable and Comparator

- **Comparable**: Used to define the natural ordering of objects. The class must implement `Comparable<T>` and override the `compareTo` method.
- **Comparator**: Used to define an external ordering of objects. A separate class can implement `Comparator<T>` and override the `compare` method.

```java
class MyClass implements Comparable<MyClass> {
    @Override
    public int compareTo(MyClass other) {
        return this.value - other.value;
    }
}

class MyComparator implements Comparator<MyClass> {
    @Override
    public int compare(MyClass o1, MyClass o2) {
        return o1.value - o2.value;
    }
}
```

### Generics Usage

Generics provide a way to create classes, interfaces, and methods that operate on types specified by the programmer. This adds type safety and reduces the need for type casting.

```java
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123); // Compile-time error
```

### When to Use Threads and Implementations

Threads are used to perform concurrent tasks. In Java, you can create a thread by:

- Extending the `Thread` class
- Implementing the `Runnable` interface
- Implementing the `Callable` interface
- Using the `ExecutorService`

```java
class MyThread extends Thread {
    public void run() {
        // task code
    }
}

class MyRunnable implements Runnable {
    public void run() {
        // task code
    }
}
```

### Java Versions: 8 vs 17

Java 8 introduced lambdas, streams, and the new Date-Time API. Java 17 is an LTS (Long-Term Support) release with features like pattern matching for switch, sealed classes, and a preview of the foreign function and memory API.

### Functional Interface

A functional interface is an interface with exactly one abstract method, making it eligible for lambda expressions and method references.

```java
@FunctionalInterface
interface MyFunction {
    void apply();
}
```

### Multiple Properties Files in Spring

You can have multiple properties files in a Spring application. You can specify them using the `@PropertySource` annotation or in the `application.properties` file.

```java
@PropertySource("classpath:application.properties")
@PropertySource("classpath:additional.properties")
```

### Specifying Different Environments

Different environments (development, testing, production) can be specified using profiles in Spring.

```java
# application-dev.properties
spring.profiles.active=dev
# application-prod.properties
spring.profiles.active=prod
```

### Use the `@Profile` annotation to specify beans for different profiles.

The `@Profile` annotation in Spring allows you to define beans that should only be created in specific profiles. This is useful for configuring different beans for different environments, such as development, testing, and production. Here’s a short guide on how to use the `@Profile` annotation to specify beans for different profiles.

### Step-by-Step Guide

1. **Define Profiles in the Configuration Class:**
   - Use `@Profile` annotation on the configuration class or individual beans.

```java
@Configuration
public class AppConfig {

    @Bean
    @Profile("development")
    public DataSource devDataSource() {
        // Configuration for development DataSource
    }

    @Bean
    @Profile("production")
    public DataSource prodDataSource() {
        // Configuration for production DataSource
    }
}
```

2. **Activate Profiles:**
   - Profiles can be activated via property files, command line, or programmatically.

**Using Property Files (application.properties or application.yml):**

```properties
spring.profiles.active=development
```

**Using Command Line:**

```sh
java -jar myapp.jar --spring.profiles.active=development
```

**Programmatically:**

```java
public class Application {
    public static void main(String[] args) {
        SpringApplication app = new SpringApplication(Application.class);
        app.setAdditionalProfiles("development");
        app.run(args);
    }
}
```

3. **Example Bean Definitions with Profiles:**

```java
@Configuration
public class DataSourceConfig {

    @Bean
    @Profile("development")
    public DataSource devDataSource() {
        HikariDataSource dataSource = new HikariDataSource();
        dataSource.setJdbcUrl("jdbc:h2:mem:devdb");
        dataSource.setUsername("dev");
        dataSource.setPassword("dev");
        return dataSource;
    }

    @Bean
    @Profile("production")
    public DataSource prodDataSource() {
        HikariDataSource dataSource = new HikariDataSource();
        dataSource.setJdbcUrl("jdbc:mysql://prod-db:3306/proddb");
        dataSource.setUsername("prod");
        dataSource.setPassword("prod");
        return dataSource;
    }
}
```

4. **Run the Application with Specific Profile:**

```sh
# For development profile
java -jar myapp.jar --spring.profiles.active=development

# For production profile
java -jar myapp.jar --spring.profiles.active=production
```

By using the `@Profile` annotation, you can easily manage different beans and configurations for various environments, ensuring that your application behaves appropriately based on the active profile.

### Using multiple databases in a single Spring Boot application

#### Step 1: Add Dependencies

Ensure you have the required dependencies for the databases in your `pom.xml` or `build.gradle` file.

For example, if you are using MySQL and PostgreSQL:

```xml
<!-- MySQL Dependency -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

<!-- PostgreSQL Dependency -->
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
</dependency>

<!-- Spring Data JPA Dependency -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

#### Step 2: Configure Data Sources

Define the data sources in the `application.properties` or `application.yml` file.

For `application.properties`:

```properties
# Primary Data Source (MySQL)
spring.datasource.primary.url=jdbc:mysql://localhost:3306/db1
spring.datasource.primary.username=root
spring.datasource.primary.password=root
spring.datasource.primary.driver-class-name=com.mysql.cj.jdbc.Driver

# Secondary Data Source (PostgreSQL)
spring.datasource.secondary.url=jdbc:postgresql://localhost:5432/db2
spring.datasource.secondary.username=postgres
spring.datasource.secondary.password=postgres
spring.datasource.secondary.driver-class-name=org.postgresql.Driver
```

#### Step 3: Define Configuration Classes

Create separate configuration classes for each data source.

##### Primary Data Source Configuration (MySQL):

```java
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
    basePackages = "com.example.repository.primary",
    entityManagerFactoryRef = "primaryEntityManagerFactory",
    transactionManagerRef = "primaryTransactionManager"
)
public class PrimaryDataSourceConfig {

    @Primary
    @Bean(name = "primaryDataSource")
    @ConfigurationProperties(prefix = "spring.datasource.primary")
    public DataSource primaryDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Primary
    @Bean(name = "primaryEntityManagerFactory")
    public LocalContainerEntityManagerFactoryBean primaryEntityManagerFactory(
            EntityManagerFactoryBuilder builder,
            @Qualifier("primaryDataSource") DataSource dataSource) {
        return builder
                .dataSource(dataSource)
                .packages("com.example.model.primary")
                .persistenceUnit("primary")
                .build();
    }

    @Primary
    @Bean(name = "primaryTransactionManager")
    public PlatformTransactionManager primaryTransactionManager(
            @Qualifier("primaryEntityManagerFactory") EntityManagerFactory primaryEntityManagerFactory) {
        return new JpaTransactionManager(primaryEntityManagerFactory);
    }
}
```

##### Secondary Data Source Configuration (PostgreSQL):

```java
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
    basePackages = "com.example.repository.secondary",
    entityManagerFactoryRef = "secondaryEntityManagerFactory",
    transactionManagerRef = "secondaryTransactionManager"
)
public class SecondaryDataSourceConfig {

    @Bean(name = "secondaryDataSource")
    @ConfigurationProperties(prefix = "spring.datasource.secondary")
    public DataSource secondaryDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Bean(name = "secondaryEntityManagerFactory")
    public LocalContainerEntityManagerFactoryBean secondaryEntityManagerFactory(
            EntityManagerFactoryBuilder builder,
            @Qualifier("secondaryDataSource") DataSource dataSource) {
        return builder
                .dataSource(dataSource)
                .packages("com.example.model.secondary")
                .persistenceUnit("secondary")
                .build();
    }

    @Bean(name = "secondaryTransactionManager")
    public PlatformTransactionManager secondaryTransactionManager(
            @Qualifier("secondaryEntityManagerFactory") EntityManagerFactory secondaryEntityManagerFactory) {
        return new JpaTransactionManager(secondaryEntityManagerFactory);
    }
}
```

#### Step 4: Create Entity Classes

Create entity classes for each database in their respective packages.

For example, in the primary database package:

```java
package com.example.model.primary;

import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class PrimaryEntity {
    @Id
    private Long id;
    private String name;

    // getters and setters
}
```

And in the secondary database package:

```java
package com.example.model.secondary;

import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class SecondaryEntity {
    @Id
    private Long id;
    private String description;

    // getters and setters
}
```

#### Step 5: Create Repository Interfaces

Create repository interfaces for each database in their respective packages.

For example, in the primary database repository package:

```java
package com.example.repository.primary;

import com.example.model.primary.PrimaryEntity;
import org.springframework.data.jpa.repository.JpaRepository;

public interface PrimaryRepository extends JpaRepository<PrimaryEntity, Long> {
}
```

And in the secondary database repository package:

```java
package com.example.repository.secondary;

import com.example.model.secondary.SecondaryEntity;
import org.springframework.data.jpa.repository.JpaRepository;

public interface SecondaryRepository extends JpaRepository<SecondaryEntity, Long> {
}
```

#### Step 6: Use the Repositories in Your Services

You can now autowire and use these repositories in your service classes to interact with both databases.

For example:

```java
@Service
public class MyService {

    @Autowired
    private PrimaryRepository primaryRepository;

    @Autowired
    private SecondaryRepository secondaryRepository;

    public void performOperations() {
        // Interact with primary database
        PrimaryEntity primaryEntity = new PrimaryEntity();
        primaryEntity.setName("Primary Name");
        primaryRepository.save(primaryEntity);

        // Interact with secondary database
        SecondaryEntity secondaryEntity = new SecondaryEntity();
        secondaryEntity.setDescription("Secondary Description");
        secondaryRepository.save(secondaryEntity);
    }
}
```

### Handling a scenario in Jenkins where one of the 10 stories has bugs.

#### 1.Identify the Issue:

Review CI/CD pipeline logs to pinpoint the failing story.

#### 2. Isolate the Faulty Change:

Use feature flags to disable the problematic feature if possible.
Alternatively, revert the specific commit causing the issue.

#### 3. Fix the Issue:

Assign the issue to the responsible developer for a fix.
Use a separate branch or hotfix branch for the fix if necessary.

#### 4. Re-run the Pipeline:

After isolation or fixing, re-run the CI/CD pipeline to ensure all other changes work correctly.

#### 5. Deploy Successfully:

If the pipeline passes, proceed with deployment.
Ensure the problematic change is either removed or fixed.

### How to use SonarQube to do the code review with peers

#### Reviewing Results:

- Access the SonarQube dashboard to review issues, code smells, vulnerabilities, and duplications.

#### Peer Review Process:

- Use analysis results in code review meetings.
- Discuss and address identified issues with peers.
- Assign issues to developers directly from SonarQube.

#### Define Quality Gates:

- Set quality gates in SonarQube based on team standards (e.g., code coverage, bug count).

#### Enforce Quality Gates:

- Ensure code cannot be merged if it fails to meet quality gates.
- Show SonarQube results directly in pull requests using pull request decorations in your version control system (e.g., GitHub, Bitbucket, GitLab).
