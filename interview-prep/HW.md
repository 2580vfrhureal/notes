## Homework1

<img src="images/java-collection-hierarchy.png" alt="java-collection-hierarchy
" width="600" height="400">

**1.List vs Set**

- **List (A great helper for dealing with order):** The stored elements are ordered and can be repeated.

- **Set (Focusing on uniqueness):** The stored elements cannot be repeated.

- **Queue (The queue system implementing queueing function):** Determines the order based on specific queueing rules; the stored elements are ordered and can be repeated.

- **Map (The expert in searching with keys):** Uses key-value pairs for storage, similar to the mathematical function y=f(x), where "x" represents the key and "y" represents the value. Keys are unordered and cannot be repeated, values are unordered and can be repeated, and each key maps to at most one value.

**2.LinkedList vs ArrayList**

- **Thread-Safety:** Both ArrayList and LinkedList are not synchronized, meaning they are not thread-safe.

- **Underlying Data Structure:**

  - **ArrayList:** Uses an array of Object.
  - **LinkedList:** Uses a doubly linked list structure.

- **Impact of Element Position on Insertion and Deletion:**

  - **ArrayList:** Uses an array for storage, so the time complexity for inserting and deleting elements depends on their positions.
    - For example, when using the `add(E e)` method, ArrayList will add the specified element to the end of the list, resulting in a time complexity of O(1). However, if you need to specify a position for insertion or deletion (`add(int index, E element)`), the time complexity becomes O(n) because elements after the specified position need to be shifted forward or backward by one position.
  - **LinkedList:** Uses a linked list for storage, so insertion and deletion at the head or tail do not depend on the position.
    - Methods like `addFirst(E e)`, `addLast(E e)`, `removeFirst()`, and `removeLast()` have a time complexity of O(1). However, if a position is specified for insertion or deletion (`add(int index, E element)`, `remove(Object o)`, `remove(int index)`), the time complexity is O(n) because the list needs to be traversed to the specified position for the operation.

- **Support for Random Access:**

  - **LinkedList:** Does not support efficient random access to elements.
  - **ArrayList:** Supports efficient random access (implements the `RandomAccess` interface), allowing quick access to elements by index using the `get(int index)` method.

- **Space Overhead:**
  - **ArrayList:** The primary space overhead comes from reserving a certain amount of capacity in the array list's structure.
  - **LinkedList:** Each element requires more space compared to ArrayList because each node stores both data and pointers to the next and previous nodes (due to the linked list structure).

**3.What is Map Interface**

<img src="images/map-interface.png" alt="map-interface
" width="600" height="400">

- We can implement maps in Java from two interfaces: Map and SortedMap. The SortedMap interface extends the Map interface. There are three classes to implement maps. These three classes are HashMap, LinkedHashMap, and TreeMap.
- The Java Map interface maintains three sets: keys, values, and key/values maps (mapping). It is possible to access all these sets individually.
- The Map interface in Java can be used with the classes that implement it, to perform various operations. Some of the primary operations we can perform on the maps in Java are:

  - Adding elements
  - Removing elements
  - Changing elements
  - Iterating through the map

**4.How does HashMap work**

- Before JDK 1.8, HashMap used an array and linked list combination for storing entries.

  - The location to store an element was determined by hashing the key and then using the formula `(n - 1) & hash` (where `n` is the array length).
  - If a collision occurred (i.e., two keys hash to the same index), a linked list was used to store the entries at that index.
  - If the keys were the same, the value was updated; if not, the new entry was added to the linked list.

- After JDK 1.8, HashMap improved its collision handling.
  - If a bucket's linked list grows beyond a certain threshold (default is 8), it gets converted into a red-black tree, which offers faster search times than a linked list.
  - However, before converting to a tree, if the array size is less than 64, the array is resized instead.
  - This reduces the likelihood of needing a tree and optimizes performance.

**5.What is hash collision**

A hash collision occurs when two different keys in a hash table (like a HashMap) produce the same hash value and thus map to the same index in the underlying array. This means that both keys would be stored in the same bucket.

1. **Hash Function**: A hash function converts a key into a hash code, which is then used to determine the index in the array where the value will be stored.

2. **Collision**: When two different keys produce the same hash code, they map to the same index in the array, leading to a collision.

**Handling Hash Collisions**:

- **Chaining**: This is the method used before JDK 1.8 and involves storing colliding entries in a linked list at the same index.
- **Open Addressing**: This involves finding another empty slot within the array through probing.

- **Treeification**: Starting from JDK 1.8, if a bucket's linked list exceeds a certain length (default is 8), it is transformed into a red-black tree for better performance.

**6.What is Collections used for**

Java Collections offer a more flexible and efficient way to store multiple data objects compared to arrays. The Java Collections framework includes various classes and interfaces that can handle different types and quantities of objects, providing a wide range of operations. The advantages of Java Collections over arrays include:

1. **Dynamic Sizing**: Collections can grow or shrink in size dynamically, unlike arrays which have a fixed size.
2. **Generics Support**: Collections support generics, allowing for type-safe data storage and retrieval.
3. **Built-in Algorithms**: Collections come with built-in methods for sorting, searching, and manipulating data.

**7.What is immutable class**

An immutable class is a class in programming whose instances cannot be modified after they are created. Once an immutable object is initialized with a set of values (its state), that state cannot be changed. Immutable classes are particularly useful in situations where you want to ensure that an object's state remains constant throughout its lifetime, which can help in writing safer, more predictable code.

### Characteristics of Immutable Classes:

1. **State cannot be modified**: The state of an immutable object is set during its creation and cannot be changed afterwards.

2. **Thread-safe**: Immutable objects are inherently thread-safe because their state cannot be altered once created.

3. **Simplicity**: They are often simpler to understand and use, as they do not have mutable state and side effects.

### How to Create an Immutable Class:

To create an immutable class, you typically follow these guidelines:

1. **Declare the class as `final`**: This prevents other classes from extending it, which could potentially add mutable behavior through subclassing.

2. **Make fields `private` and `final`**: This ensures that fields cannot be accessed or modified directly from outside the class and prevents them from being reassigned once initialized.

3. **Do not provide setter methods**: Since you want to prevent modification of the object's state after creation, do not provide any methods that modify the state of the object.

4. **Ensure mutable fields are deeply copied or made immutable**: If your class contains references to mutable objects (e.g., collections), ensure that those objects are either deeply copied during construction or encapsulated in a way that prevents external modification.

5. **Constructors for initialization**: Provide constructors or factory methods that initialize all the fields of the object. Once the object is initialized, its state remains constant.

6. **Avoid mutable return types**: If your class has methods that return references to mutable objects (like arrays or collections), make sure those objects are also immutable or are not shared externally.

### Example of Immutable Class with a Collection:

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

In this updated example:

- `name` and `age` remain `private final` to ensure they are immutable.
- `hobbies` is also declared `private final`, indicating that it cannot be reassigned after initialization.
- In the constructor, `hobbies` is either assigned a defensive copy of the provided list (`new ArrayList<>(hobbies)`), or in this case, an unmodifiable view of the list (`Collections.unmodifiableList(hobbies)`). Using `Collections.unmodifiableList()` ensures that the `hobbies` list cannot be modified externally after the `ImmutablePerson` object is created.

**8.HashTable vs HashMap vs ConcurrentHashmap**

**9.String vs StringBuilder vs StringBuffer**
**10.Comparator vs Comparable, when to use which one**
**11.Overriding vs overloading**
**12.JRE vs JDK vs JVM**
**13.Java 8 basic data types**
**14.Primitive type, reference type**
