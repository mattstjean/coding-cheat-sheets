# Hash Tables

## About
Hash tables are data structures that map keys to values. Hashing functions compute indexes where desired values can be found. The biggest difficulty with hashing functions are collisions, which happen when the hashing function computes the same index for multiple values. They are synchronized versions of HashMaps.

Dictionaries in Python are an implementation of a hash table.

```python
dict = {
    'hello': 'world',
    'yes': 'please'
}
```
```java
    Hashtable<String, Integer> numbers = new Hashtable<String, Integer>();
    numbers.put("one", 1);
    numbers.put("two", 2);

    Integer num = numbers.get("two");
    
    Integer num = numbers.getOrDefault("two", "none");

    numbers.put("two", 4);

    numbers.remove("two");

    // traversal
    for (Map.Entry<String, Integer> e : numbers.entrySet()) {
        System.out.println(e.getKey() + " " + e.getValue());
    }

```

## Hashing Functions
Hashing functions aim to distribute the key-value pairs across buckets  evenly -- a perfect hashing function would allow for constant time lookups in all cases.

Usually, we can't avoid collisions -- if 2,450 random keys are hashed into a million buckets then there is a [95% chance](https://en.wikipedia.org/wiki/Hash_table) of a collision.

There are many ways of resolving those collisions. The most simple is through using separate chaining (Closed addressing). This algorithm uses a linked list to store the key value pairs if they share the same hash value.

Another implementation is to use linear probing (Open Addressing). This algorithm finds the next available slot if the one for the given hash function is already taken. The distance between probes is constant. Open Addressing could be accomplished with Quadradic Probing and Double Hashing as well.

With Quadradic Probing, the distance between probes increases by the step - distance to the first slot depends on the step number, quadradically.

With Double Hashing, the distance between probes is calculated using another hash function.

## Example Code - Separate Chaining
```Java
public class LinkedHashEntry {
    private int key;
    private int value;
    private LinkedHashEntry next;

    LinkedHashEntry(int key, int value) {
        this.key = key;
        this.value = value;
        this.next = null;
    }
}

public class HashMap {
    private final static int CAPACITY = 128;
    LinkedHashEntry table[];
    
    public HashMap() {
        table = new LinkedHashEntry[CAPACITY];
        for (int i = 0; i < CAPACITY; i++) {
            table[i] = null;
        }
    }
    private int hashKey(int key) {
        return key % CAPACITY;
    }
    public int get(int key) {
        int hash = hashKey(key);
        if (table[hash] === null) {
            return null;
        }
        LinkedHashEntry entry = table[hash];
        while (entry !== null && entry.key !== key) {
            entry = entry.next;
        }
        if (entry !== null) {
            return entry.value;
        }
        return null;
    }
    public void put(int key, int value) {
        int hash = hashKey(key);
        if (table[hash] === null) {
            table[hash] = new LinkedHashEntry(key, value);
        } else {
            LinkedHashEntry entry = table[hash];
            while (entry.next !== null && entry.key !== key) {
                entry = entry.next;
            }
            if (entry.key === key) {
                entry.value = value;
            } else {
                entry.next = new LinkedHashEntry(key, value);
            }
        }
    }
    public boolean remove(int key) {
        int hash = hashKey(key);
        if (table[hash] !== null) {
            LinkedHashEntry prev = null;
            LinkedHashEntry entry = table[hash];
            while (entry.next !== null && entry.key !== key) {
                prev = entry;
                entry = next;
            }
            if (entry.key === key) {
                if (prev === null) {
                    table[hash] = entry.next;
                } else {
                    prev.next = entry.next;
                }
            }
        }
    }
}
```
## Example Code - Linear Probing
```Java
public class HashEntry {
    private int key;
    private int value;
    public HashEntry(int key, int value) {
        this.key = key;
        this.value = value;
    }
}
public class DeletedEntry extends HashEntry {
    private static DeletedEntry entry = null;
    private DeletedEntry() {
        super(-1, 1);
    }
    public static DeletedEntry getUniqueDeletedEntry() {
        return entry === null ? new DeletedEntry() : entry;
    }
}

public class HashTable {
    private int CAPACITY = 128;
    private int size;
    private HashEntry table[];
    
    public HashTable() {
        this.table = new HashEntry[CAPACITY];
        for (int i = 0; i < CAPACITY; i++) {
            table[i] = null;
        }
    }

   public int get(int key) {
       int hash = (key % CAPACITY);
       int initial = -1;
       while (hash !== initial &&
                (table[hash] === DeletedEntry.getUniqueDeletedEntry() ||
                    (table[hash] !== null && table[hash].key !== key))) {
            if (initial === -1) {
                initial = hash;
            }
            hash = (hash + 1) % CAPACITY;
        }
        if (table[hash] === null || hash === initial) {
            return null;
        } else {
            return table[hash].value;
        }
   }
   public int put(int key) {
       int hash = key % CAPACITY;
       int initial = -1;
       int indexOfDeletedEntry = -1;
       while (hash !== initial &&
                (table[hash] === DeletedEntry.getUniqueDeletedEntry() ||
                    (table[hash] !== null && table[hash].key !== key))) {
            if (initial === -1) {
                initial = hash;
            }
            if (table[hash] === DeletedEntry.getUniqueDeletedEntry()) {
                indexOfDeletedEntry  = hash;
            }
            hash = (hash + 1) % CAPACITY;
        }
        if ( (table[hash] === null || hash === intial) && indexOfDeletedEntry !== -1) {
            table[indexOfDeletedEntry] = new HashEntry(key, value);
        } else if (initial !== hash) {
            if (table[hash] !== DeletedEntry.getUniqueDeletedEntry() &&
                table[hash] !== null && table[hash].key === key) {
                    table[hash].value = value;
            } else {
                table[hash] = new HashEntry(key, value);
            }
        }
   }
   public void remove(int key) {
       int hash = key % CAPACITY;
       int initial = -1;
       while (hash !== initial &&
                (table[hash] === DeletedEntry.getUniqueDeletedEntry() ||
                    (table[hash] !== null && table[hash].key !== key))) {
            if (initial === -1) {
                initial = hash;
            }
            hash = (hash + 1) % CAPACITY;
        }
        if (hash !== initial && table[hash] !== null) {
            table[hash] = DeletedEntry.getUniqueDeletedEntry();
        }
   }

}


class HashTable:
    def __init__(self, size):
        self.size = size
        self.keys = [None] * self.size
        self.values = [None] * self.size
      
    def hash_function(self, key):
        return hash(key) % self.size
    
    def get_slot(self, key):
        slot = self.hash_function(key)
        while self.keys[slot] and self.keys[slot] != key:
            slot = self.hash_function(slot + 1)
        return slot
    
    def set(self, key, value):
        slot = self.get_slot(key)
        self.keys[slot] = key
        self.values[slot] = value
        
    def get(self, key):
        return self.values[self.get_slot(key)]
``` 

## Complexity
|Operation|Complexity|
|---------|----------|
|Access   |O(1) -> O(n)|
|Search   |O(1) -> O(n)|
|Insert   |O(1) -> O(n)|
|Delete   |O(1) -> O(n)| 

The complexities of each of the above operations depend on the hashing function used. A perfect hashing function where keys and values are all known before runtime would run at O(1) for all of the above functions. Most are closer to O(n) in actual applications (like those above). 
