# Hash Table

## Understanding the problem

When writing a program, we often need to **map** different data types together, such as the roll number of all students in a class. We need some data structure that stores the mapping between data of different types. The names of all students are strings, while their roll numbers might be positive integer values.

One way to store these mappings is in two separate arrays at the same indices.

![[Pasted image 20251019191843.png]]

This is an easy way to store data, but what if we want to retrieve the roll number of a student by their name? If the data is stored in arrays, we will have to traverse the entire `names` array to search for a student's name to get their roll number.

This will solve the problem at hand. However, the operation does a linear scan of the entire array, which will be inefficient if many students are in a class. What if we want to store the roll numbers of all the students in all classes of all the schools in a city? This is not an efficient way to store data.

### Limitations of storing mappings in two arrays

- **Bad performance:** Searching for data stored in an array has linear **O(N)** worst case time complexity.
- **Fixed size:** The size of an array is fixed at the time of creation and cannot be expanded/reduced.

## Real life example

A real-life example of such a data structure is a phone book directory with the phone numbers of all the residents in a city. The phone book lists the names in alphabetical order. Anyone can quickly jump to the page with a person's phone number just by looking at the index instead of linearly scanning the entire phonebook.

This fast access is possible because the index translates the name to the page number(intermediate value), where the phone number is stored super fast. Once we know the name, we apply a few steps to find the page number and then look at that page for the phone number.

![[Pasted image 20251019192054.png]]

## Logical representation

A hash table is logically represented as a simple table where each row stores a mapping between a key and a value. This representation is easy to understand and use when solving a problem.

## Defining a hash function

### Mathematical function

In pure mathematics, a function from set K to V is defined as the logic that assigns exactly one value in V to every element in K. The set K is the **domain**, and V is the function's **codomain**. In simple terms, a mathematical function is essentially something that maps values from a set K to a set V. These sets can have data of any type (integers, strings, objects, etc.).

![[Pasted image 20251019192343.png]]

### Hash function

 A hash function is a mathematical function that can map elements from an arbitrary (infinite or fixed) set to a finite site. Any mathematical function with a fixed-size codomain set (hash value) can be called a hash function. The domain set (keys) for the hash function can be of a fixed or infinite size.

**==Not all mathematical functions are hash functions, but all hash functions are mathematical functions==**. The output from a hash function (elements of the codomain set) is called hash values, sometimes also called hash codes, digests, or simply hashes.

![[Pasted image 20251019192527.png]]

### Collision

A hash function's domain set (keys) can be potentially infinite, but the co-domain set (hash values) has a fixed size. It should be easy to see that no matter how good a hash function is, mapping a potentially infinite number of values to values in a finite size will result in a collision.

> When two different elements in a hash function's domain set(keys) map to the same value in the codomain set (hash value), it is said to be a collision.

![[Pasted image 20251019192735.png]]

The primary purpose of a hash function is to map elements in a large (potentially infinite) set to a fixed-sized set, so collision is inevitable. However, we can choose the hash function carefully to reduce the chances of collision. A good hash function has a low probability for collision and is fast.

## Properties of a good hash function

A good hash function for a specific type of input data (domain set) may perform poorly for other data types.

### Uniformity

A good hash function maps elements in the domain set(keys) to elements in the co-domain set(hash values) as uniformly as possible. Some hash functions, like the mod function, are uniform. **==In a perfectly uniform function, every element in the co-domain set should be mapped to the same number of elements in the domain set.==**

![[Pasted image 20251019192955.png]]

### Deterministic

A hash function should be deterministic. This means that any element in the domain set(keys) should be mapped to exactly one element in the co-domain set(hash values) and always be the same. Essentially, this means that for a given input(key), the hash function should always result in the same hash value.

## Efficient

A hash function maps input data (keys) to a fixed-sized set of values(hash value). The primary purpose of a hash function is to store and retire data items using this computed hash value, so the hash value computation should be efficient.

## Internal mechanics of a hash table

A hash table is generally an encapsulation around an array, and the basic principle on which it works is quite simple. We know that accessing a data item in an array is a constant time **O(1)** operation if we know the index where the data item is stored.

We can leverage an array's fast random-access property to map a key and value together. We can store the original key-value pair at that index by using a hash function that converts the given key into an array's index(hash value). A good hash function guarantees that a given key will always result in the same index, and the computation is a constant-time operation. Once we fix the index for a key, the data can be accessed in constant time in the array.

### Internal array

A hash table is just an encapsulation around an array. This array stores the actual data (key and value). This internal array generally has a fixed size, but more complex implementations can also use a dynamic array. The internal array's size also decides which hash function to use, as the hash function ultimately calculates an index in this array. The internal array's size depends on the distribution of keys and use case and it should be big enough to prevent too many collisions.

### Hash function

The hash function is the heart of a hash table. It converts a key into an index of the internal array. The hash function for a hash table should be fast, deterministic, and have a uniformly distributed set of output values to prevent collision. Even though a hash function might be mathematically uniform if used with skewed input(keys), it might still lead to a collision, so it should be chosen with the use case in mind.

### Collision resolusion

No matter how good a hash function is, there will be chances of collisions if the domain set (unique key values) is large.

A hash table also encapsulates a collision resolution mechanism for such cases. This mechanism transparently decides how to handle collisions so that the data is not lost and the operations on the hash table are still efficient.

![[Pasted image 20251019194009.png]]

## Supported Operations

### Insert operation

The insert operation is one of the primary operations on a hash table and is used to store a key-value mapping. A key-value mapping is stored by hashing the key to get the index in the internal array and storing the key-value pair at that location. If the key is already present in the table, its value is updated to the new value.

### Search operation

The search operation is another primary operation on a hash table and is used to retrieve the mapped value for a given key. The value is retrieved by passing the given key to the hash function to get the index in the internal array and fetching the value at that location. If the value key-value mapping does not exist, the search function returns an error value to indicate it or throws an error.

### Delete operation

The delete operation deletes the key-value mapping for a given key from the hash table. The given key is passed to the hash function to get its index in the internal array, and the value at that location is deleted. If the value key-value mapping does not exist, the operation is treated as a no-op(nothing done)

# Separate Chaining

 Separate chaining is one such way of collision resolution in hash tables. As the name suggests, the internal array is an array of a chain-like data structure in the separate chaining implementation of a hash table. This data structure can simultaneously hold more than one data item, which is exactly how collisions are resolved. All the keys with the same hash value are stored at the hashed index, forming a data chain.

![[Pasted image 20251019202139.png]]

Separate chaining is sometimes called **closed addressing** or **open hashing** because collisions are handled using another data structure (a linked list). 

## Advantages

The separate chaining implementation can easily resolve collision in hash tables and is the most intuitive way to solve this problem. It has a few advantages over other collision resolution schemes that we will learn later in this course.

> - **Easy**: Separate chaining is easier to understand and implement than other collision resolution schemes, which we will learn later.
> - **Infinite size**: There is no restriction on the hash table size. The chain data structure can grow as much as memory permits.
> - **Collision performance**: Unlike other collision resolution schemes, in separate chaining, collision on one hashed index does not affect the other hashed indices.

## Limitations

Even though the separate chaining implementation is easy to understand and intuitive, it is not always the best choice for implementing hash tables. It has a few limitations over other collision resolution schemes.

> - **Infinite size**: No size restriction can lead to unchecked hash table expansion, causing out-of-memory (OOM) issues.
> - **Extra space**: The data structure used for chaining has its data members, such as previous and next references, in doubly linked lists that use extra space.
> - **CPU cache performance**: When using a chain data structure, the data is scattered throughout the memory, and so the CPU cache performance is poor as it cannot leverage the locality of reference as in arrays.

## Key components

The hash table is just an encapsulation around an array of linked lists that stores key-value pairs. Different pieces have to be put together to create a hash table

### Record

Each linked list node stores the key-value pair that represents the mapping in the separate chaining implementation of a hash table. A record is a data structure encapsulating this key-value pair, making it easy to use and operate. Each node in the linked list holds data in this format.

![[Pasted image 20251019202657.png]]

```java
// Represents an entry in the hash table
class Record {

    int key;

    int value;

    Record(int key, int value) {
        this.key = key;
        this.value = value;
    }
}

  

// Definition for doubly-linked list.
class ListNode {

    Record val;

    ListNode prev;

    ListNode next;

    ListNode() {}

    ListNode(Record val) { this.val = val; }
};
```

## Internal array

In the separate chaining implementation of a hash table, the internal array is an array of linked lists. Each index in the array represents a hash value, and the linked list at the index stores all the records that have keys with the same hash value(collision).

![[Pasted image 20251019202913.png]]

When a hash table is created, all linked lists are empty. Adding mappings to the hash table adds new nodes to the linked lists at the hashed indices.

![[Pasted image 20251019202934.png]]

```java
// Import the LinkedList class

import java.util.LinkedList;

// An array of linked list where the

// node stores data of type Record

List<LinkedList<Record>> table;

// Initialize the table with the given capacity
table = new ArrayList<>(capacity);

for (int i = 0; i < capacity; i++) {

    table.add(new LinkedList<>());

}
```

### Hash function

The hash function is the heart of any hash table. It converts a given key to an index (hash value) in the internal array. The key-value pair is searched, inserted, or deleted in the internal array at that index. Any hash-value collision is resolved using separate chaining (adding to the linked list).

![[Pasted image 20251019203257.png]]

```java
// Implementation of a hash function for this hash table
int hashFunction(int key) {
    return key % capacity;
}
```

## the Hash Table Class



![[Pasted image 20251019203351.png]]

```java
import java.util.*;

// Represents an entry in the hash table
class Record {
    int key;
    int value;

    Record(int key, int value) {
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The hashtable
    private List<LinkedList<Record>> table;
    private int capacity;

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with the given capacity
        table = new ArrayList<>(capacity);
        for (int i = 0; i < capacity; i++) {
            table.add(new LinkedList<>());
        }
    }

    public int search(int key) {}

    public void insert(int key, int value) {}

    public void remove(int key) {}
}
```

## Search operation

The search operation is one of the primary operations on a hash table and is used to retrieve the value of a key as stored in the hash table.

### Algorithm

The search operation is quite simple. We only need to calculate the index (hash code) for the given key and then search for the key at the index. However, the hash table could have a collision for the given key (another key with the same hash code stored in the table), so we must follow a separate chaining scheme to search for the given key.

Once we calculate the index (hash code) for the given key, we start a linear search in the linked list at that index until we either find the key or the linked list is traversed completely. If the given key is found in the table, we return it. Otherwise, we return a flag (`-1` in this example) to indicate that the key is absent.

![[Pasted image 20251019204028.png]]

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Search for the key in the list at the calculated index.
- **Step 3:** If the key is found, return it's value. Otherwise, return `-1`.

```java

private int hashFunction(int key) {
	return key % capacity;
}
    
 public int search(int key) {
        // Get the bucket index
        int index = hashFunction(key);
        
        // Search for the key in the bucket
        for (Record entry : table.get(index)) {
            if (entry.key == key) {
                // Return the value if key is found
                return entry.value;
            }
        }
        // Return -1 if the key is not found
        return -1;
    }
```


## Insert Operation

If the key is already in the hash table, the insert operation updates its value to the new value supplied. The implementation is encapsulated in the insert function, which uses separate chaining to search for the key first. Let us look at the algorithm and implementation of the insert operation in a hash table implemented using separate chaining.

### Algorithm

The insert operation is just an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the linked list at that index for a record with the given key. We need to consider two cases.

#### 1. Key is present in the table

If a record with the given key is found in the linked list at the calculated index with the given key, its value is updated to the new value.

![[Pasted image 20251019204619.png]]

> **Algorithm**
> 
> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Search for the key in the list at the calculated index.
> - **Step 3:** If the key is found, update the value of the stored record.

#### 1. Key is not present in the table

If no record with the given key is found in the linked list at the calculated index. A new record with the given key-value pair is created and inserted at the **end** of the linked list.

**Why do we insert the node at the end?**

Since the key was not found during the search, we have already reached the end of the list. Thus, we can simply insert the new node there.

![[Pasted image 20251019204731.png]]

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Search for the key in the list at the calculated index.
- **Step 3:** If the key is not found, add a new node with the key-value pair at the end of the list.

```java

private int hashFunction(int key) {
    return key % capacity;
}

public void insert(int key, int value) {
    // Get the bucket index
    int index = hashFunction(key);
    // Check if the key already exists and update its value
    for (Record entry : table.get(index)) {
        if (entry.key == key) {
            // Update value if key exists
            entry.value = value;
            return;
        }
    }
    // Add a new record if the key does not exist
    table.get(index).add(new Record(key, value));
}
```

## Delete Operation

If the key is not in the hash table, it is a no-op(nothing is done). The implementation is encapsulated in the delete function, which uses separate chaining to search for the key first. Let us look at the algorithm and implementation of the delete operation in a hash table implemented using separate chaining.

### Algorithm

The delete operation is also an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the linked list at that index for a record with the given key. We need to consider two cases.

#### 1. Key is present in the table

If a record is found in the linked list at the calculated index that has the given key, the node where it is stored is deleted from the linked list using the standard node deletion algorithm in a linked list. The resultant list is then stored at the calculated index.

![[Pasted image 20251019205356.png]]

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Search for the key in the list at the calculated index.
- **Step 3:** Delete the node if it is found and store the resultant list at the calculated index.

#### 2. Key is not present in the table

Nothing is done if no record is found in the linked list at the calculated index with the given key, and the delete operation becomes a no-op (nothing done).


```java
private int hashFunction(int key) {
    return key % capacity;
}

public void remove(int key) {
    // Get the bucket index
    int index = hashFunction(key);
    // Remove the record with the matching key
    table.get(index).removeIf(entry -> entry.key == key);
}
```


```java
import java.util.*;

// Represents an entry in the hash table
class Record {
    int key;
    int value;

    Record(int key, int value) {
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The hashtable
    private List<LinkedList<Record>> table;
    private int capacity;

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with the given capacity
        table = new ArrayList<>(capacity);
        for (int i = 0; i < capacity; i++) {
            table.add(new LinkedList<>());
        }
    }

    private int hashFunction(int key) {
        return key % capacity;
    }

    public int search(int key) {
        // Get the bucket index
        int index = hashFunction(key);
        // Search for the key in the bucket
        for (Record entry : table.get(index)) {
            if (entry.key == key) {
                // Return the value if key is found
                return entry.value;
            }
        }
        // Return -1 if the key is not found
        return -1;
    }

    public void insert(int key, int value) {
        // Get the bucket index
        int index = hashFunction(key);
        // Check if the key already exists and update its value
        for (Record entry : table.get(index)) {
            if (entry.key == key) {
                // Update value if key exists
                entry.value = value;
                return;
            }
        }
        // Add a new record if the key does not exist
        table.get(index).add(new Record(key, value));
    }

    public void remove(int key) {
        // Get the bucket index
        int index = hashFunction(key);
        // Remove the record with the matching key
        table.get(index).removeIf(entry -> entry.key == key);
    }

    public List<Integer> getKeysAtIndex(int index) {
        // Return an empty list if the index is invalid
        if (index < 0 || index >= capacity) {
            return new ArrayList<>();
        }
        // Collect all keys in the bucket
        List<Integer> keys = new ArrayList<>();
        for (Record entry : table.get(index)) {
            keys.add(entry.key);
        }
        return keys;
    }
}
```


# Linear Probing

ne major disadvantage of separate chaining schemes is that the table size is not limited. Because the chain data structure is scattered(non-contiguous) throughout the memory, it does not benefit from the locality of reference.

In the linear probing scheme, the internal array stores the key-value pair. The size of the internal array limits the size of the hash table. Because the array is a contiguous memory, it has performance benefits due to the locality of reference.

## Handling collisions

When two keys have the same hash value (index), they are stored consecutively, one after the other. This means the first colliding key is stored at the correct hash index. All other colliding keys are stored at array indices representing other hash values.

![[Pasted image 20251020103201.png]]

The linear probing search is generally performed up to N iterations, where N is the size of the array. A modulo operator makes the traversal circular to keep the result within the array's bounds. The collision resolution scheme can be summarized as follows:

> **Insert**
> 
> - **Step 1:** Find the hash value for the given key.
> - **Step 2:** Start a linear search from the hashed index to find an unoccupied slot.
> - **Step 3:** Insert the key-value pair at the slot.
> 
> **Search**
> 
> - **Step 1:** Find the hash value for the given key.
> - **Step 2:** Start a linear search from the hashed index to find the key.
> - **Step 3:** Return the value if the key is found.

## Key components

### Record

**==Unlike separate chaining, in a linear probing implementation of a hash table, each index in the internal array stores only one record, and collisions are handled by finding the next available free slot.==** For this reason, we store the key-value mapping and additional metadata to identify the type of slot(empty, deleted, or occupied) at each index in the array.

![[Pasted image 20251020103542.png]]

```java
// Represents the state of a record in the hash table

enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {

    // Use the separately defined RecordType enum

    RecordType state = RecordType.EMPTY;

    int key = 0;

    int value = 0;

    Record() {}

    Record(int key, int value) {

        this.state = RecordType.OCCUPIED;

        this.key = key;

        this.value = value;
    }
}
```

### Internal array

In the linear probing implementation of a hash table, the internal array stores all the data, so it is an array of records. Each slot in this array is either an empty or deleted record, as described by its `recordType` data member.

```java
// The hash table implemented as a list of Records
List<Record> table;


// Initialize the table with empty records
table = new ArrayList<>();
for (int i = 0; i < capacity; i++) {
    table.add(new Record());
}
```

### Hash function

The hash function is the heart of any hash table. It converts a given key to an index (hash value) in the internal array. The key-value pair is then searched, inserted, or deleted in the internal array at that index. Any collision in hash values is resolved using the linear probing method.

![[Pasted image 20251020103745.png]]

```java
// Implementation of a hash function for this hash table
int hashFunction(int key) {
    return key % capacity;
}
```

## the Hash Table Class

![[Pasted image 20251020104119.png]]

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // The hash table implemented as a list of Records
    private List<Record> table;

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public int search(int key) {}

    public boolean insert(int key, int value) {}

    public void remove(int key) {}
}
```

## Search Operation

We only need to calculate the index (hash code) for the given key and then search for the key at the index. However, the hash table could have a collision for the given key, so we follow the linear probing scheme to search for it.

Once we calculate the index (hash code) for the given key, we start a linear search in the array from that index until we either find an occupied record with the given key, hit an empty record, or traverse the entire internal array. Let us look at the different cases separately to understand how the search operation is implemented in a hash table that uses a linear probing scheme for collision resolution

### 1. The key is present in the table

If the key is already in the hash table, we will find it when we start a linear search from the hashed index in the internal array. Once we find it, we return the value of this key.

![[Pasted image 20251020105301.png]]

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Do a linear search in the array from the calculated index.
- **Step 3:** If the key is found, return it's value.

### 2. An empty slot is found

If the key is not present in the hash table and the table is not full, we will hit an empty record when we start a linear search from the hashed index in the internal array. We return a flag (`-1` in this example) to indicate that the key is absent.

![[Pasted image 20251020105340.png]]

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Do a linear search in the array from the calculated index.
- **Step 3:** If an `EMPTY` slot is found while searching, return `-1`.

### 3. The key is not present and the hash table is full

If the key is not present in the hash table and the table is full, we will fully traverse the internal array when we start a linear search from the hashed index in the internal array and not hit any empty record. In this case, we return `-1` to indicate that the key is not in the hash table.

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Do a linear search in the array from the calculated index.
- **Step 3:** If the key is not found even after searching the entire array, return `-1`.

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // The hash table implemented as a list of Records
    private List<Record> table;

    // Primary hash function: Computes the index as key % capacity
    private int hashFunction(int key) {
        return key % capacity;
    }

    private int probeForOccupiedIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is occupied and matches the key
            if (
                table.get(probeIndex).state == RecordType.OCCUPIED &&
                table.get(probeIndex).key == key
            ) {
                return probeIndex;
            }
        }
        // Return -1 if no matching record is found
        return -1;
    }

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public int search(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Return the value if found, otherwise -1
        return occupiedIndex == -1 ? -1 : table.get(occupiedIndex).value;
    }
}
```

## Insert operation

The insert operation is just an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the internal array for the given key starting from that index. We need to consider three cases.

### 1. Key is present in the table

In this case, an occupied record with the given key is found when searching the internal array using linear probing starting from the calculated index. We update the value of that record to the new value and return it as `true`

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Traverse and search the array from that index using linear probing.
- **Step 3:** If the key is found, update the value of the stored record and return `true`.

### 2. An unoccupied slot is found

In this case, the internal array is searched linearly starting from the calculated index, and no occupied record with the given key is found. Still, we hit an unoccupied (`EMPTY` or `DELETED`) slot. This means the hash table did not store the key, so we updated the unoccupied record found with the key-value pair and marked it occupied. We return `true` to indicate that the insert operation succeeded.

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Traverse and search the array from that index using linear probing.
- **Step 3:** If an unoccupied (`EMPTY` or `DELETED`) slot is found, update the record with the given key-value pair, mark it `OCCUPIED`, and return `true`.

### 3. The internal array is full

In this case, the internal array is searched linearly starting from the calculated index, but no record of the given key is found in the entire traversal. This means that the internal array is full. We return  `false` to indicate that the insert operation failed.

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Traverse and search the array from that index using linear probing.
- **Step 3:** If no unoccupied slot is found, return `false`.

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // The hash table implemented as a list of Records
    private List<Record> table;

    // Primary hash function: Computes the index as key % capacity
    private int hashFunction(int key) {
        return key % capacity;
    }

    private int probeForOccupiedIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is occupied and matches the key
            if (
                table.get(probeIndex).state == RecordType.OCCUPIED &&
                table.get(probeIndex).key == key
            ) {
                return probeIndex;
            }
        }
        // Return -1 if no matching record is found
        return -1;
    }

    private int probeForEmptyIndex(int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is available (either EMPTY or DELETED)
            if (table.get(probeIndex).state != RecordType.OCCUPIED) {
                return probeIndex;
            }
        }
        // Return -1 if no available slot is found
        return -1;
    }

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public boolean insert(int key, int value) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Update the value if the key exists
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).value = value;
            return true;
        }
        // Find an empty slot to insert the new key-value pair
        int emptyIndex = probeForEmptyIndex(startIndex);
        if (emptyIndex != -1) {
            table.set(emptyIndex, new Record(key, value));
            return true;
        }
        // Return false if the table is full and insertion fails
        return false;
    }
}
```

## Delete Operation

The delete operation is also an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the internal array for a record with the given starting from the calculated index. We may need to consider three cases.

### 1. Key is present in the table

In this case, the key is found in an occupied record when searching the internal array using linear probing starting from the calculated index. We update the record to mark it `DELETED`. This deleted record can be reused when inserting a new key-value pair in the hash table. The search operation only terminates at an empty record, so it skips any deleted records.

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Traverse and search the array from that index using linear probing.
- **Step 3:** If the key is found, mark the slot `DELETED`

### 2. An empty slot is found

Suppose the key is not found in any occupied record when searching the internal array using quadratic probing from the calculated index. In that case, the delete operation becomes a no-op (nothing is done). This can happen if we reach an empty record before finding the key.

### 3. The internal array is full

In this case, the internal array is searched linearly, starting from the calculated index. Still, neither an unoccupied record nor a record with the given key is found in the entire traversal. This means that the internal array is full. In this case, the delete operation becomes a no-op (nothing done).

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // The hash table implemented as a list of Records
    private List<Record> table;

    // Primary hash function: Computes the index as key % capacity
    private int hashFunction(int key) {
        return key % capacity;
    }

    private int probeForOccupiedIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is occupied and matches the key
            if (
                table.get(probeIndex).state == RecordType.OCCUPIED &&
                table.get(probeIndex).key == key
            ) {
                return probeIndex;
            }
        }
        // Return -1 if no matching record is found
        return -1;
    }

    private int probeForEmptyIndex(int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is available (either EMPTY or DELETED)
            if (table.get(probeIndex).state != RecordType.OCCUPIED) {
                return probeIndex;
            }
        }
        // Return -1 if no available slot is found
        return -1;
    }

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }


    public void remove(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Mark the slot as DELETED
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).state = RecordType.DELETED;
        }
    }
}
```



```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // The hash table implemented as a list of Records
    private List<Record> table;

    // Primary hash function: Computes the index as key % capacity
    private int hashFunction(int key) {
        return key % capacity;
    }

    private int probeForOccupiedIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is occupied and matches the key
            if (
                table.get(probeIndex).state == RecordType.OCCUPIED &&
                table.get(probeIndex).key == key
            ) {
                return probeIndex;
            }
        }
        // Return -1 if no matching record is found
        return -1;
    }

    private int probeForEmptyIndex(int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Linear probing
            int probeIndex = (startIndex + i) % capacity;
            // Check if the slot is available (either EMPTY or DELETED)
            if (table.get(probeIndex).state != RecordType.OCCUPIED) {
                return probeIndex;
            }
        }
        // Return -1 if no available slot is found
        return -1;
    }

    public MyHashTable(int capacity) {
        this.capacity = capacity;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public int search(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Return the value if found, otherwise -1
        return occupiedIndex == -1 ? -1 : table.get(occupiedIndex).value;
    }

    public boolean insert(int key, int value) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Update the value if the key exists
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).value = value;
            return true;
        }
        // Find an empty slot to insert the new key-value pair
        int emptyIndex = probeForEmptyIndex(startIndex);
        if (emptyIndex != -1) {
            table.set(emptyIndex, new Record(key, value));
            return true;
        }
        // Return false if the table is full and insertion fails
        return false;
    }

    public void remove(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Mark the slot as DELETED
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).state = RecordType.DELETED;
        }
    }

    public int getKeyAtIndex(int index) {
        return table.get(index).state == RecordType.OCCUPIED
            ? table.get(index).key
            : -1;
    }
}
```

# Quadratic Probing

Like linear probing, the internal array stores the key-value pair in a quadratic probing scheme. The size of the internal array limits the size of the hash table, and because the array has contiguous memory, it has performance benefits due to the locality of reference.

## Handling collisions

Unlike linear probing, in quadratic probing, when two keys have the same hash value (index), they are stored non-consecutively in the array. The distance between each collision increases exponentially and is determined by a quadratic function. It calculates the index for the ith collision for any hashed value

![[Pasted image 20251021111116.png]]

Like linear probing, the first colliding key is stored at the correct hash index, while all other colliding keys are stored at indices in the array representing some other hash value. Unlike linear probing, though, since the colliding values are separated by exponentially increasing distances, primary clustering is avoided.

![[Pasted image 20251021111156.png]]

Like linear probing, the quadratic probing search is generally performed up to N iterations, where N is the size of the array. A modulo operator makes the traversal circular to keep the result within the array's bounds. The collision resolution scheme can be summarized as follows:

> **Insert**
> 
> - **Step 1:** Find the hash value for the given key
> - **Step 2:** Iterate up to N times using the quadratic function to calculate the index until an unoccupied slot is found.
> - **Step 3:** For each iteration, calculate the index using a quadratic equation and iterate until an unoccupied slot is found
> - **Step 4:** Insert the key-value pair at the slot.
> 
> **Search**
> 
> - **Step 1:** Find the hash value for the given key
> - **Step 2:** Iterate up to N times using the quadratic function to calculate the index until the key or an unoccupied slot is found.
> - **Step 3:** Return the value if the key is found

## Key components

### Record

Like linear probing, in a quadratic probing implementation of a hash table, each index in the internal array stores only one record, and collisions are handled by finding the next available free slot using quadratic probing. For this reason, at each index in the array, we store the key-value mapping and additional metadata to identify the type of slot(empty, deleted, or occupied).

![[Pasted image 20251020103542.png]]

### Internal array

In the quadratic probing implementation of a hash table, the internal array stores all the data, so it is an array of records. Each slot in this array is either an empty or deleted record, as described by its ``recordType`` data member.

![[Pasted image 20251021111448.png]]

### Hash function

The hash function is the heart of any hash table. It is a function that converts a given key to an index (hash value) in the internal array. The key value pair is then searched, inserted, or deleted in the internal array at that index. Any collision in hash values is resolved using the quadratic probing method.

![[Pasted image 20251020103745.png]]

### Quadratic function

A hash table implemented using quadratic probing uses a quadratic function to calculate the index of the ith collision starting from the hashed index. This quadratic function is critical to implementing the hash table and has to be fine-tuned, just like the hash function. This function calculates the probe sequence when there is a collision. It calculates the index for the ith collision for a hashed value.


## Hash Table Class

![[Pasted image 20251021111817.png]]

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // Quadratic probing constants
    private int a, b;
    // The hash table implemented as a list of Records
    private List<Record> table;

    public MyHashTable(int capacity, int a, int b) {
        this.capacity = capacity;
        this.a = a;
        this.b = b;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public int search(int key) {}

    public boolean insert(int key, int value) {}

    public void remove(int key) {}
}
```
## Search operation

### Algorithm

The search operation is quite simple: We only need to calculate the index (hash code) for the given key and then search for the key at the index. However, the hash table could have a collision for the given key, so we follow the quadratic probing scheme to search for it.

Once we calculate the index (hash code) for the given key, we search the array starting from that index using the quadratic function until we find an occupied record with the given key, hit an empty record, or finish the probe sequence. Let us look at the different cases separately to understand how the search operation is implemented in a hash table that uses a quadratic probing scheme for collision resolution.

#### 1. The key is present in the table

If the key is already in the hash table, we will find it when searching for it using quadratic probing in the internal array. Once we find it, we return the value of this key.

![[Pasted image 20251021112339.png]]

> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Search the array using quadratic probing from the calculated index.
> - **Step 3:** If the key is found, return it's value.

#### 2. An empty slot is found

If the key is not present in the hash table and the probe sequence is not full, we will hit an empty record when we search for it using quadratic probing in the internal array. We return a flag (`-1` in this example) to indicate that the key is absent.

> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Search the array using quadratic probing from the calculated index.
> - **Step 3:** If an `EMPTY` slot is found while probing, return `-1`.

#### 3. The key is not present and the probe sequence is full

If the key is not present in the hash table and the entire probe sequence for that key is full, we will finish the entire quadratic probe starting from the hashed index and not hit any empty record. In this case, we return `-1` to indicate that the key is not in the hash table

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Search the array using quadratic probing from the calculated index.
- **Step 3:** If the key is not found and the probe sequence is full, return `-1`.

```java
private int hashFunction(int key) {
    return key % capacity;
}

private int probeForOccupiedIndex(int key, int startIndex) {
    for (int i = 0; i < capacity; ++i) {
        // Quadratic probing
        int probeIndex = (startIndex + a * i * i + b * i) % capacity;
        // Check if the slot is occupied and matches the key
        if (
            table.get(probeIndex).state == RecordType.OCCUPIED &&
            table.get(probeIndex).key == key
        ) {
            return probeIndex;
        }
    }
    // Return -1 if no matching record is found
    return -1;
}

public int search(int key) {
    // Compute the initial index using the primary hash function
    int startIndex = hashFunction(key);
    // Find the occupied index for the key
    int occupiedIndex = probeForOccupiedIndex(key, startIndex);
    // Return the value if found, otherwise -1
    return occupiedIndex == -1 ? -1 : table.get(occupiedIndex).value;
}
```

## Insert operation

The insert operation is just an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the internal array for the given key starting from that index. We need to consider three cases.

### 1. Key is present in the table

In this case, an occupied record with the given key is found when searching the internal array using quadratic probing starting from the calculated index. We update the value of that record to the new value and return it as `true`.

> **Algorithm**
> 
> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Traverse and search the array from that index using quadratic probing.
> - **Step 3:** If the key is found, update the value of the stored record and return `true`.

### 2. An unoccupied slot is found

In this case, the internal array is searched using quadratic probing starting from the calculated index, and no occupied record with the given key is found. Still, we hit an unoccupied (`EMPTY` or `DELETED`) slot. This means that the hash table did not store the key, so we updated the unoccupied record found with the key-value pair and marked it occupied. We return true to indicate that the insert operation succeeded.

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Traverse and search the array from that index using quadratic probing.
- **Step 3:** If an unoccupied (`EMPTY` or `DELETED`) slot is found, update the record with the given key-value pair, mark it `OCCUPIED`, and return `true`.

### 3. The probe sequence is full

In this case, the internal array is searched using quadratic probing starting from the calculated index, but no record of the given key is found in the entire traversal. This means that the internal array is full. We return `false` to indicate that the insert operation failed.

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Traverse and search the array from that index using quadratic probing.
- **Step 3:** If no unoccupied slot is found, return `false`.

```java
public boolean insert(int key, int value) {
    // Compute the initial index using the primary hash function
    int startIndex = hashFunction(key);
    // Find the occupied index for the key
    int occupiedIndex = probeForOccupiedIndex(key, startIndex);
    // Update the value if the key exists
    if (occupiedIndex != -1) {
        table.get(occupiedIndex).value = value;
        return true;
    }
    // Find an empty slot to insert the new key-value pair
    int emptyIndex = probeForEmptyIndex(startIndex);
    if (emptyIndex != -1) {
        table.set(emptyIndex, new Record(key, value));
        return true;
    }
    // Return false if the table is full and insertion fails
    return false;
}
```

## Delete operation

### 1. Key is present in the table

In this case, the key is found in an occupied record when searching the internal array using quadratic probing starting from the calculated index. We update the record to mark it `DELETED`. This deleted record can be reused when inserting a new key-value pair in the hash table. The search operation only terminates at an empty record, so it skips any deleted records.

> **Algorithm**
> 
> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Traverse and search the array from that index using quadratic probing.
> - **Step 3:** If the key is found, mark the slot `DELETED`.

### 2. An empty slot is found

Suppose the key is not found in any occupied record when searching the internal array using quadratic probing from the calculated index. In that case, the delete operation becomes a no-op (nothing is done). This can happen if we reach an empty record before finding the key.

### 3. The probe sequence is full

If the key is not present in the hash table and the entire probe sequence for that key is full, we will finish the entire quadratic probe starting from the hashed index and not hit any empty record. In this case, the delete operation becomes a no-op (nothing done).

```java
public void remove(int key) {

        // Compute the initial index using the primary hash function

        int startIndex = hashFunction(key);

        // Find the occupied index for the key

        int occupiedIndex = probeForOccupiedIndex(key, startIndex);

        // Mark the slot as DELETED

        if (occupiedIndex != -1) {
            table.get(occupiedIndex).state = RecordType.DELETED;
        }
    }
```

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // Quadratic probing constants
    private int a, b;
    // The hash table implemented as a list of Records
    private List<Record> table;

    // Primary hash function: Computes the index as key % capacity
    private int hashFunction(int key) {
        return key % capacity;
    }

    private int probeForOccupiedIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Quadratic probing
            int probeIndex = (startIndex + a * i * i + b * i) % capacity;
            // Check if the slot is occupied and matches the key
            if (
                table.get(probeIndex).state == RecordType.OCCUPIED &&
                table.get(probeIndex).key == key
            ) {
                return probeIndex;
            }
        }
        // Return -1 if no matching record is found
        return -1;
    }

    private int probeForEmptyIndex(int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Quadratic probing
            int probeIndex = (startIndex + a * i * i + b * i) % capacity;
            // Check if the slot is available (either EMPTY or DELETED)
            if (table.get(probeIndex).state != RecordType.OCCUPIED) {
                return probeIndex;
            }
        }
        // Return -1 if no available slot is found
        return -1;
    }

    public MyHashTable(int capacity, int a, int b) {
        this.capacity = capacity;
        this.a = a;
        this.b = b;
        // Initialize the table with empty records
        table = new ArrayList<>();
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public int search(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Return the value if found, otherwise -1
        return occupiedIndex == -1 ? -1 : table.get(occupiedIndex).value;
    }

    public boolean insert(int key, int value) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Update the value if the key exists
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).value = value;
            return true;
        }
        // Find an empty slot to insert the new key-value pair
        int emptyIndex = probeForEmptyIndex(startIndex);
        if (emptyIndex != -1) {
            table.set(emptyIndex, new Record(key, value));
            return true;
        }
        // Return false if the table is full and insertion fails
        return false;
    }

    public void remove(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Mark the slot as DELETED
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).state = RecordType.DELETED;
        }
    }

    public int getKeyAtIndex(int index) {
        return table.get(index).state == RecordType.OCCUPIED
            ? table.get(index).key
            : -1;
    }
}
```

# Double Hashing

 It is a slight variation of quadratic probing that has all its advantages but reduces the secondary clustering problem by having a different probe sequence for colliding keys.

Like quadratic probing, in a double hashing scheme, the internal array stores the key-value pair. The size of the internal array limits the size of the hash table, and because the array has contiguous memory, it has performance benefits due to the locality of reference.

## Handling collisions

In quadratic probing, when two keys have the same hash value (index), they follow the same probe sequence defined by the quadratic function, which leads to the secondary clustering problem.

**==In double hashing, the probe sequence is decided by another hash function. When there is a collision in hash values for two keys in the first hash function, the second hash function calculates the step size for probing. If the two hash functions are correctly chosen, it is very unlikely that the two colliding keys will have the same probe step size. This way, the chances of any clustering (primary or secondary) is minimized in a double hashing implementation.==**

![[Pasted image 20251021122610.png]]

Like quadratic probing, the first colliding key is stored at the correct hash index, while all other colliding keys are stored at indices in the array that represent some other hash value. However, unlike linear and quadratic probing, the chances of primary or secondary clustering are minimized since another hash function decides the distance between the colliding values.

![[Pasted image 20251021122650.png]]

Just like linear and quadratic probing, the probe in double hashing is generally performed up to N iterations, where N is the size of the array. A modulo operator makes the traversal circular to keep the result within the array's bounds. The collision resolution scheme can be summarized as follows:

> **Insert**
> 
> - **Step 1:** Find the hash value for the given key
> - **Step 2:** Calculate step size using the second hash function
> - **Step 3:** Iterate up to N times in the step size calculated above until an unoccupied slot is found
> - **Step 4:** Insert the key-value pair at the slot.
> 
> **Search**
> 
> - **Step 1:** Find the hash value for the given key
> - **Step 2:** Calculate step size using the second hash function
> - **Step 3:** Iterate up to N times in the step size calculated above until the key or an unoccupied slot is found
> - **Step 4:** Return the value if the key is found


## Key Components

### Record

Like quadratic probing, in a double hashing implementation of a hash table, each index in the internal array stores only one record, and collisions are handled by finding the next available free slot. For this reason, we store the key-value mapping and additional metadata to identify the type of slot(`empty`, `deleted`, or `occupied`) at each index in the array.

![[Pasted image 20251020103542.png]]

### Internal array

In the double hashing implementation of a hash table, the internal array stores all the data, so it is an array of records. Each slot in this array is either an empty or deleted record, as described by its ``recordType`` data member. We will learn later why it is important to distinguish between these two states.

### Hash function

The hash function is the heart of any hash table. It is a function that converts a given key to an index (hash value) in the internal array. The key value pair is then searched, inserted, or deleted in the internal array at that index. Any collision in hash values is resolved using the double hashing method.


![[Pasted image 20251020103745.png]]


### Second hash function

**==A hash table implemented using double hashing uses a second hash function to calculate the step size for probing when the hashed index is occupied. This second hash function is critical to implementing the hash table and has to be fine-tuned, just like the hash function. The main goal of the second hash function is to ensure that the probe sequence for two colliding keys is not the same to prevent secondary clustering. Since it is also just a hash function, it can also have collisions, but if carefully chosen, the chances of clustering are very low compared to linear and quadratic probing.==**

![[Pasted image 20251021122840.png]]

## Hash Table Class

![[Pasted image 20251021123353.png]]

```java
import java.util.*;

// Represents the state of a record in the hash table

enum RecordType {

    EMPTY,

    DELETED,

    OCCUPIED

}


// Represents an entry in the hash table
class Record {

    // Use the separately defined RecordType enum

    RecordType state = RecordType.EMPTY;

    int key = 0;

    int value = 0;

    Record() {}

    Record(int key, int value) {

        this.state = RecordType.OCCUPIED;

        this.key = key;

        this.value = value;
    }
}

class MyHashTable {

    // The total number of slots in the hash table

    private int capacity;

    // A prime number used for double hashing

    private int hashPrime;

    // The hash table implemented as a list of Records

    private List<Record> table;

    public MyHashTable(int capacity, int hashPrime) {

        this.capacity = capacity;

        this.hashPrime = hashPrime;

        this.table = new ArrayList<>(capacity);

        for (int i = 0; i < capacity; i++) {

            table.add(new Record());
        }
    }

  

    public int search(int key) {}

  

    public boolean insert(int key, int value) {}

  

    public void remove(int key) {}

}
```

## Search Operation

### Algorithm

Once we calculate the index (hash code) for the given key, we search the array starting from that index in increments of step size calculated by the second hash function until we either find an occupied record with the given key, hit an empty record, or finish the probe sequence.  Let us look at the different cases separately to understand how the search operation is implemented in a hash table that uses a double hashing scheme for collision resolution.

#### 1. The key is present in the table

If the key is already in the hash table, we will find it when searching for it using double hashing in the internal array. Once we find it, we return the value of this key.

> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Calculate the step size for the key using the second hash function.
> - **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
> - **Step 4:** If the key is found, return it's value.

#### 2. An empty slot is found

If the key is not present in the hash table and the probe sequence is not full, we will hit an empty record when we search for it using double hashing in the internal array. We return a flag (`-1` in this example) to indicate that the key is absent.

> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Calculate the step size for the key using the second hash function.
> - **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
> - **Step 4:** If an `EMPTY` slot is found while probing, return `-1`.

#### 3. The key is not present and the probe sequence is full

This case is very unlikely, as two hash functions should provide sufficient randomness (different starting points and probe sequences) for two keys. However, there is still a slight chance that the probe sequence might be full due to stored mappings for other hashes or the full hash table. In this case, we return `-1` to indicate that the key is not in the hash table.

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Calculate the step size for the key using the second hash function.
- **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
- **Step 4:** If the key is not found and the probe sequence is full, return `-1`.

```java
// Primary hash function: Computes the index as key % capacity
private int hashFunction1(int key) {
    return key % capacity;
}

// Secondary hash function: Used for probing during collisions
// Returns hashPrime - (key % hashPrime), ensuring a different step
// size
private int hashFunction2(int key) {
    return hashPrime - (key % hashPrime);
}

private int probeForOccupiedIndex(int key, int startIndex) {
    for (int i = 0; i < capacity; ++i) {
        // Double hashing
        int probeIndex =
            (startIndex + i * hashFunction2(key)) % capacity;
        // Check if the slot is occupied and matches the key
        if (
            table.get(probeIndex).state == RecordType.OCCUPIED &&
            table.get(probeIndex).key == key
        ) {
            return probeIndex;
        }
    }
    // Return -1 if no matching record is found
    return -1;
}

public int search(int key) {
    // Compute the initial index using the primary hash function
    int startIndex = hashFunction1(key);
    // Find the occupied index for the key
    int occupiedIndex = probeForOccupiedIndex(key, startIndex);
    // Return the value if found, otherwise -1
    return occupiedIndex == -1 ? -1 : table.get(occupiedIndex).value;
}
```

## Insert operation

### Algorithm

The insert operation is just an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the internal array in the step size calculated by the second hash function. We need to consider three cases.

#### 1. Key is present in the table

In this case, an occupied record with the given key is found when searching the internal array using double hashing starting from the calculated index. We update the value of that record to the new value and return `true`

> **Algorithm**
> 
> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Calculate the step size for the key using the second hash function.
> - **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
> - **Step 4:** If the key is found, update the value of the stored record and return `true`.

#### 2. An unoccupied slot is found

In this case, the internal array is searched using double hashing, and no occupied record with the given key is found, but we hit an unoccupied (`EMPTY` or `DELETED`) slot. This means that the hash table did not store the key, so we updated the unoccupied record found with the key-value pair and marked it occupied. We return a `true` value to indicate that the insert operation succeeded.

> **Algorithm**
> 
> - **Step 1:** Calculate the index(hash code) for the given key.
> - **Step 2:** Calculate the step size for the key using the second hash function.
> - **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
> - **Step 4:** If an unoccupied (`EMPTY` or `DELETED`) slot is found, update the record with the given key-value pair, mark it occupied, and return `true`.

#### 3. The probe sequence is full

This case is unlikely, as two hash functions should provide sufficient randomness (different starting points and probe sequences) for two keys. However, there is still a slight chance that the probe sequence might be full due to stored mappings for other hashes or the full hash table.

In this case, the entire probe sequence starting from the hashed index is finished, but no record of the given key is found. We return `false` to indicate that the insert operation failed.

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Calculate the step size for the key using the second hash function.
- **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
- **Step 4:** If no unoccupied slot is found, return `false`.

```java
public boolean insert(int key, int value) {
    // Compute the initial index using the primary hash function
    int startIndex = hashFunction1(key);
    // Find the occupied index for the key
    int occupiedIndex = probeForOccupiedIndex(key, startIndex);
    // Update the value if the key exists
    if (occupiedIndex != -1) {
        table.get(occupiedIndex).value = value;
        return true;
    }
    // Find an empty slot to insert the new key-value pair
    int emptyIndex = probeForEmptyIndex(key, startIndex);
    if (emptyIndex != -1) {
        table.set(emptyIndex, new Record(key, value));
        return true;
    }
    // Return false if the table is full and insertion fails
    return false;
}

private int hashFunction1(int key) {
    return key % capacity;
}

// Secondary hash function: Used for probing during collisions
// Returns hashPrime - (key % hashPrime), ensuring a different step
// size
private int hashFunction2(int key) {
    return hashPrime - (key % hashPrime);
}

private int probeForOccupiedIndex(int key, int startIndex) {
    for (int i = 0; i < capacity; ++i) {
        // Double hashing
        int probeIndex =
            (startIndex + i * hashFunction2(key)) % capacity;
        // Check if the slot is occupied and matches the key
        if (
            table.get(probeIndex).state == RecordType.OCCUPIED &&
            table.get(probeIndex).key == key
        ) {
            return probeIndex;
        }
    }
    // Return -1 if no matching record is found
    return -1;
}

private int probeForEmptyIndex(int key, int startIndex) {
    for (int i = 0; i < capacity; ++i) {
        // Double hashing
        int probeIndex =
            (startIndex + i * hashFunction2(key)) % capacity;
        // Check if the slot is available (either EMPTY or DELETED)
        if (table.get(probeIndex).state != RecordType.OCCUPIED) {
            return probeIndex;
        }
    }
    // Return -1 if no available slot is found
    return -1;
}
```

## Delete operation

### Algorithm

The delete operation is also an extension of the search operation. Like the search operation, we calculate the index (hash code) for the given key and search the internal array for a record with the given starting from the calculated index. We may need to consider three cases.

#### 1. Key is found

In this case, double hashing finds the key in an occupied record when searching the internal array. We update the record to mark it `DELETED`. This deleted record can be reused when inserting a new key-value pair in the hash table. The search operation only terminates at an empty record, so it skips any deleted records.

**Algorithm**

- **Step 1:** Calculate the index(hash code) for the given key.
- **Step 2:** Calculate the step size for the key using the second hash function.
- **Step 3:** Start searching the array from the calculated index in step size calculated by the second hash function.
- **Step 4:** If the key is found, mark it `DELETED`.

#### 2. An empty slot is found

Suppose the key is not found in any occupied record when searching the internal array using double hashing from the calculated index. In that case, the delete operation becomes a no-op (nothing is done). This can happen if we reach an `empty` record before finding the key.

#### 3. The probe sequence is full

This case is unlikely, as two hash functions should provide sufficient randomness (different starting points and probe sequences) for two keys. However, there is still a slight chance that the probe sequence might be full due to stored mappings for other hashes or the full hash table.

Nothing is done if the entire probe sequence starting from the hashed index is finished but no record with the given key is found. In this case, the delete operation becomes a no-op (nothing done).

```java
 public void remove(int key) {

        // Compute the initial index using the primary hash function

        int startIndex = hashFunction1(key);

        // Find the occupied index for the key

        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Mark the slot as DELETED

        if (occupiedIndex != -1) {

            table.get(occupiedIndex).state = RecordType.DELETED;
        }
    }
```

```java
import java.util.*;

// Represents the state of a record in the hash table
enum RecordType {
    EMPTY,
    DELETED,
    OCCUPIED
}

// Represents an entry in the hash table
class Record {
    // Use the separately defined RecordType enum
    RecordType state = RecordType.EMPTY;
    int key = 0;
    int value = 0;

    Record() {}

    Record(int key, int value) {
        this.state = RecordType.OCCUPIED;
        this.key = key;
        this.value = value;
    }
}

class MyHashTable {
    // The total number of slots in the hash table
    private int capacity;
    // A prime number used for double hashing
    private int hashPrime;
    // The hash table implemented as a list of Records
    private List<Record> table;

    // Primary hash function: Computes the index as key % capacity
    private int hashFunction1(int key) {
        return key % capacity;
    }

    // Secondary hash function: Used for probing during collisions
    // Returns hashPrime - (key % hashPrime), ensuring a different step
    // size
    private int hashFunction2(int key) {
        return hashPrime - (key % hashPrime);
    }

    private int probeForOccupiedIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Double hashing
            int probeIndex =
                (startIndex + i * hashFunction2(key)) % capacity;
            // Check if the slot is occupied and matches the key
            if (
                table.get(probeIndex).state == RecordType.OCCUPIED &&
                table.get(probeIndex).key == key
            ) {
                return probeIndex;
            }
        }
        // Return -1 if no matching record is found
        return -1;
    }

    private int probeForEmptyIndex(int key, int startIndex) {
        for (int i = 0; i < capacity; ++i) {
            // Double hashing
            int probeIndex =
                (startIndex + i * hashFunction2(key)) % capacity;
            // Check if the slot is available (either EMPTY or DELETED)
            if (table.get(probeIndex).state != RecordType.OCCUPIED) {
                return probeIndex;
            }
        }
        // Return -1 if no available slot is found
        return -1;
    }

    public MyHashTable(int capacity, int hashPrime) {
        this.capacity = capacity;
        this.hashPrime = hashPrime;
        this.table = new ArrayList<>(capacity);
        for (int i = 0; i < capacity; i++) {
            table.add(new Record());
        }
    }

    public int search(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction1(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Return the value if found, otherwise -1
        return occupiedIndex == -1 ? -1 : table.get(occupiedIndex).value;
    }

    public boolean insert(int key, int value) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction1(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Update the value if the key exists
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).value = value;
            return true;
        }
        // Find an empty slot to insert the new key-value pair
        int emptyIndex = probeForEmptyIndex(key, startIndex);
        if (emptyIndex != -1) {
            table.set(emptyIndex, new Record(key, value));
            return true;
        }
        // Return false if the table is full and insertion fails
        return false;
    }

    public void remove(int key) {
        // Compute the initial index using the primary hash function
        int startIndex = hashFunction1(key);
        // Find the occupied index for the key
        int occupiedIndex = probeForOccupiedIndex(key, startIndex);
        // Mark the slot as DELETED
        if (occupiedIndex != -1) {
            table.get(occupiedIndex).state = RecordType.DELETED;
        }
    }

    public int getKeyAtIndex(int index) {
        return table.get(index).state == RecordType.OCCUPIED
            ? table.get(index).key
            : -1;
    }
}
```

# Pattern: Counting

The counting technique iterates through the sequence while maintaining the count (frequency) of data items seen so far in a hash table.

The counting technique is quite simple and easy to understand. Consider we are given a string `s` and we need to count the frequency of all characters. We initialize a hash map `frequency` to map a character to its frequency and iterate the array from start to end. In each iteration, we check if the current character exists in the frequency map and increment its count by one. At the end of all iterations, the frequency map will have the count of all characters in `s`.

## Algorithm

The algorithm given below outlines the technique to compute the frequency of data items in a sequence.

> **Algorithm**
> 
> - **Step 1:** Initialize a map `frequency` to map characters to an integer
> - **Step 2:** Iterate in the string or array, and for each item, do the following:
>     - **Step 2.1:** If the item exists in `frequency` map increment its count by one otherwise, set it to one


```java
  
class Solution {
    public Map<Character, Integer> countFrequency(String s) {

        // Initialize a hash map to map a character to its frequency
        Map<Character, Integer> frequency = new HashMap<>();

        // Traverse the string and store the frequency of each character in a hash map
        for (char ch : s.toCharArray()) {
            frequency.put(ch, frequency.getOrDefault(ch, 0) + 1);
        }
        return frequency;
    }
}
```

## Example  First non repeating character

Given a string **s**, write a function to find and return the index of the first non-repeating character in it. If it does not exist, return `-1`.

```java
import java.util.*;

class Solution {

    public int firstNonRepeatingCharacter(String s) {

        Map<Character, Integer> frequency = countFrequency(s);

        for (int i = 0; i < s.length(); i++) {

            if(frequency.get(s.charAt(i)) == 1)
               return i;
        }

        return -1;

    }

    private Map<Character, Integer> countFrequency(String s) {

        Map<Character, Integer> frequency = new HashMap<>();

        for(char ch: s.toCharArray()) {

            frequency.put(ch, frequency.getOrDefault(ch, 0) + 1);
        }
        	       return frequency;
    }
}
```

## Example Constructibility check

Given two strings, **s1** and **s2**, write a function that returns `true` if s1 can be constructed by using the letters from the s2 and `false` otherwise. Each letter in the s2 can only be used once in the s1.

```java
import java.util.*;

class Solution {
    public Map<Character, Integer> countFrequency(String s) {
        Map<Character, Integer> frequency = new HashMap<>();
        for (char ch : s.toCharArray()) {
            frequency.put(ch, frequency.getOrDefault(ch, 0) + 1);
        }
        return frequency;
    }

    public boolean constructibilityCheck(String s1, String s2) {
        // Create a map to store the frequency of each character in s2
        Map<Character, Integer> s2Frequency = countFrequency(s2);
        // Iterate over the characters in s1
        for (char ch : s1.toCharArray()) {
            // If the frequency of the character is zero, return false
            if (s2Frequency.getOrDefault(ch, 0) == 0) {
                return false;
            }
            // Decrement the frequency of the character in the map
            s2Frequency.put(ch, s2Frequency.get(ch) - 1);
        }
        // If all characters in s1 can be constructed from s2, return
        // true
        return true;
    }
}
```


## Example  Anagram checker

Given two strings, **s**, and **p**, write a function that returns `true` if p is an anagram of s, otherwise return `false`.

```java
import java.util.*;

class Solution {
    public Map<Character, Integer> countFrequency(String s) {
        Map<Character, Integer> frequency = new HashMap<>();
        for (char ch : s.toCharArray()) {
            frequency.put(ch, frequency.getOrDefault(ch, 0) + 1);
        }
        return frequency;
    }

    public boolean anagramChecker(String s, String t) {
        // If the strings are of different lengths, they cannot be
        // anagrams
        if (s.length() != t.length()) {
            return false;
        }
        // Create a map to store the frequency of each character in the
        // first string
        Map<Character, Integer> sFrequency = countFrequency(s);
        // Traverse the second string and decrement the frequency of each
        // character in the hash map
        for (char ch : t.toCharArray()) {
            if (!sFrequency.containsKey(ch)) {
                return false;
            }
            sFrequency.put(ch, sFrequency.get(ch) - 1);
            if (sFrequency.get(ch) == 0) {
                sFrequency.remove(ch);
            }
        }
        return sFrequency.isEmpty();
    }
}
```

## Example  Build palindrome

Given a string **s** that consists of lowercase or uppercase letters, write a function that finds and returns the length of the longest palindrome, which can be built using all or some of those letters

```java
import java.util.*;

class Solution {
    public Map<Character, Integer> countFrequency(String s) {
        Map<Character, Integer> frequency = new HashMap<>();
        for (char ch : s.toCharArray()) {
            frequency.put(ch, frequency.getOrDefault(ch, 0) + 1);
        }
        return frequency;
    }

    public int buildPalindrome(String s) {
        // Create a map to store the frequency of each character in the
        // string
        Map<Character, Integer> frequency = countFrequency(s);
        // Initialize the length of the longest palindrome
        int length = 0;
        // Initialize a boolean flag to check if there are odd counts of
        // characters
        boolean odd = false;
        // Iterate over the map to calculate the length of the longest
        // palindrome
        for (var entry : frequency.entrySet()) {
            // If the count of the character is even, add it to the
            // length
            if (entry.getValue() % 2 == 0) {
                length += entry.getValue();
            }
            // If the count of the character is odd, add the count minus
            // one to the length and set the odd flag to true
            else {
                length += entry.getValue() - 1;
                odd = true;
            }
        }
        // If there are odd counts of characters, add one to the length
        return odd ? length + 1 : length;
    }
}
```

# Pattern Generation

Every sequence of items follows an inherent pattern that can be described by the relative position of its items with each other

![[Pasted image 20251021163713.png]]

While the human mind can easily recognize such patterns in sequences based on the relative positioning of items in each sequence, it is impossible for a machine to do it. The pattern generation technique is a powerful technique that uses a hash table to assign a unique pattern string to all sequences that follow the same pattern.

![[Pasted image 20251021163729.png]]

## Pattern generation technique

The generic pattern generation technique is quite simple; it takes an input sequence and produces a pattern string that denotes the pattern that the input sequence follows. Each unique item in the input sequence is mapped to a unique value in the output string, and we use a hash map to remember these mappings.

We initialize an empty string `pattern`, a `seed` variable with some default value and a hash map `map` to map unique items in the input to characters in the pattern string. We then traverse the sequence from start to end, and for each item in the sequence, check if it is already mapped to some character in `map`. If not, we map it to the current value of `seed` in `map` and update `seed` to some new, unique value; otherwise, we use the mapped value in `map`. We then append this value at the end of the `pattern` string along with a delimiter value. A delimiter is a unique value that will never be mapped to any item in the input sequence.

At the end of all iterations `pattern` holds the string denoting the pattern followed in the input sequence.

### Delimeter

For cases where the mapped value is more than one character long, a delimiter serves the purpose of defining boundaries

![[Pasted image 20251021164312.png]]

## Algorithm

The algorithm given below outlines the generic pattern generation technique on any sequence.

> - **Step 1:** Initialize `seed` with some unique default value an empty string `pattern`
> - **Step 2:** Create a hash map `map` to map data items in a sequence to some unique value
> - **Step 3:** Iterate in the sequence from start to end, and for each `item` do the following:
> - **Step 3.1:** If `item` is not present in `map`
>     - **Step 3.1.1:** Map `item` with the current value of `seed` in the `map`
>     - **Step 3.1.2:** Update the value of `seed` to some unique value
> - **Step 3.2:** Append the value mapped to `item` in `map` to the `pattern` string


```java
public class GeneratePattern {

    public String generatePattern(List<Character> arr) {
        // A map to map characters to unique integers
        HashMap<Character, Integer> map = new HashMap<>();

        // The resulting pattern string
        StringBuilder pattern = new StringBuilder();

        // Seed to generate unique values for characters
        int seed = 0;

        // Create a mapped value based on the first occurrence of each item
        for (char item : arr) {
            if (!map.containsKey(item)) {
                map.put(item, seed++);
            }
            pattern.append(map.get(item)).append(",");
        }

        return pattern.toString();
    }
}
```

## Example  Row specific words

Given an array of string words, write a function that returns the words that can be typed using letters of the alphabet on only one row of an American keyboard like the one given below. You can return the answer in **any order**.

```java
import java.util.*;

class Solution {
    public Set<Character> getRow1() {
        return new HashSet<>(
            List.of('q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p')
        );
    }

    public Set<Character> getRow2() {
        return new HashSet<>(
            List.of('a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l')
        );
    }

    public Set<Character> getRow3() {
        return new HashSet<>(List.of('z', 'x', 'c', 'v', 'b', 'n', 'm'));
    }

    public int getRow(char c) {
        Set<Character> row1 = getRow1();
        Set<Character> row2 = getRow2();
        Set<Character> row3 = getRow3();

        if (row1.contains(c)) {
            return 1;
        }

        if (row2.contains(c)) {
            return 2;
        }

        if (row3.contains(c)) {
            return 3;
        }

        // This case won't occur as all characters are from valid rows
        return 0;
    }

    public boolean canBeTypedWithOneRow(String word) {
        // Get the row for the first character
        int row = getRow(Character.toLowerCase(word.charAt(0)));

        // Check if all characters belong to the same row
        for (char c : word.toCharArray()) {
            if (getRow(Character.toLowerCase(c)) != row) {
                return false;
            }
        }

        return true;
    }

    public List<String> rowSpecificWords(String[] words) {
        List<String> result = new ArrayList<>();

        // Iterate over each word
        for (String word : words) {
            if (canBeTypedWithOneRow(word)) {
                result.add(word);
            }
        }

        return result;
    }
}
```

## Example  Homomorphic strings

Given two strings, **s**, and **t**, write a function that returns `true` if they are homomorphic, return `false` otherwise.

Two strings, **s**, and **t,** are homomorphic if the characters in **s** can be replaced to get **t**. All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

```java
import java.util.*;

class Solution {
    public String generatePattern(String str) {
        Map<Character, Integer> charToIndex = new HashMap<>();
        StringBuilder pattern = new StringBuilder();
        int index = 0;

        // Create a mapped value based on the first occurrence of each
        // character
        for (char ch : str.toCharArray()) {
            if (!charToIndex.containsKey(ch)) {
                charToIndex.put(ch, index++);
            }
            pattern.append(charToIndex.get(ch)).append(",");
        }

        return pattern.toString();
    }

    public boolean homomorphicStrings(String s, String t) {
        // Strings of different lengths can't be homomorphic
        if (s.length() != t.length()) {
            return false;
        }

        // If the generated patterns are the same, the strings are
        // homomorphic
        return generatePattern(s).equals(generatePattern(t));
    }
}
```

## Example Pattern matching

Given a **pattern** and a string **s**, write a function that returns `true` if s follows the same pattern, otherwise return `false`.

**Follow** means a full match, such that there is a bijection between a letter in pattern and a **non-empty** word in s.

```java
import java.util.*;

class Solution {
    public List<String> stringToList(String s) {
        // Convert pattern string into a list of single-character strings
        List<String> result = new ArrayList<>();
        for (char c : s.toCharArray()) {
            result.add(String.valueOf(c));
        }
        return result;
    }

    public String generatePattern(List<String> words) {
        Map<String, Integer> wordToIndex = new HashMap<>();
        StringBuilder pattern = new StringBuilder();
        int index = 0;

        // Create a mapped value based on the first occurrence of each
        // word
        for (String word : words) {
            if (!wordToIndex.containsKey(word)) {
                wordToIndex.put(word, index++);
            }
            pattern.append(wordToIndex.get(word)).append(",");
        }

        return pattern.toString();
    }

    public boolean patternMatching(String pattern, String s) {
        // Split the string s into an array of words
        List<String> words = List.of(s.split(" "));

        // If the length of pattern and words are different, return false
        if (pattern.length() != words.size()) {
            return false;
        }

        // If the generated patterns are the same, return true
        return generatePattern(stringToList(pattern)).equals(
            generatePattern(words)
        );
    }
}
```

