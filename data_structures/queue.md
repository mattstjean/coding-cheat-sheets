# Queue

## About

A queue is a data structure that operates on a first in first out (FIFO) basis, similar to a line for a movie. The two operations that define a queue are enqueue and dequeue. Enqueue adds an item to the back of the queue, dequeue removes an item from the back of the queue. 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/300px-Data_Queue.svg.png)

Software queues are used in a lot of cases like real life queues -- they give service to the task that asked for it first. A printer, for example, usually prints the first job given to it and then queues up the others until it is their turn. Queues are also used for breadth-first searches where each vertex is traversed.


## Complexity
Some implementations use arrays or array lists, which mean that the operations have similar complexities to those of an array. Others use nodes and pointers or doubly linked lists and therefore would have similar complexities to those structures.

## Code example using an array
```Java
public class Queue {
    private int storage[];
    private int head;
    private int tail;
    private int capacity;
    private int length;

    public Queue(int size) {
        this.storage = new int[size];
        this.capacity = size;
        this.head = 0;
        this.tail = -1;
        this.length = 0;
    }
    public int dequeue() {
        if (isEmpty()) {
            return null;
        }
        int dequeueData = storage[head];
        head = head++;
        length--;
        return dequeueData;
    }
    public boolean enqueue(int data) {
        if (isFull()) {
            return false;
        }
        tail++;
        storage[tail] = data;
        length++;
    }
    public int peek() {
        if (isEmpty()) {
            return null;
        }
        return storage[head];
    }
    public boolean isEmpty() {
        return length === 0;
    }
    public boolean isFull() {
        return length === capacity;
    }
}
```
In this implementation utilizing a Java array the Big-O complexity looks like this:

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(n)      |
|Delete   |O(1)      | 

Either the insert or delete functionality will be O(n) since the insertion or deletion will occur at the beginning of the list, a procedure that isn't optimized in Java like `push` and `pop` are.

## Code example using a doubly linked list
```java
public class Node<Object> {
    public Node next;
    public Node prev;
    public Object data;

    public Node(Object val) {
        this.next = null;
        this.prev = null;
        this.data = val;
    }
    public Node(Object data, Node next) {
        this.next = next;
        this.data = data;
    }
    public Node(Object data, Node next, Node prev) {
        this.next = next;
        this.prev = prev;
        this.data = data;
    }
}

public class Queue {
    public Node head;
    public Node tail;
    public int length;

    public Queue() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    public void enqueue(data) {
        Node newNode = new Node(data, head);
        if (head === null) {
            head = newNode;
        } else {
            tail.next = newNode;
            newNode.prev = tail;
        }
        tail = newNode;
        length++;
    }
    public Object dequeue() {
        Object dequeuedData = head.data;
        head = head.next;
        length--;
        return dequeuedData;
    }
}
```

In this implementation utilizing a doubly linked list the Big-O complexity looks like this:

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      |

Insertion and deletion in this example is more efficient, though there is more data being stored (i.e. the pointers to next and prev).


## Practice Problems
* [Implement a queue using two stacks](https://www.hackerrank.com/challenges/ctci-queue-using-two-stacks)
