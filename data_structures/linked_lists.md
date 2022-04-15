# Linked Lists

## About
Linked lists are linear collections of data that consist of nodes with data and pointers. Singly linked lists have nodes that store the value of the node and a pointer to the next node. Doubly linked lists additionally store a pointer to the previous node.

Linked lists do not need to be stored contiguously in memory like an array, so insertion and deletion is relatively simple. They do not natively support accessing one data node or indexing through operations. These operations are normally performed just by looping through the nodes. They also use more memory than arrays since they also store pointers to the next link(s).

They are commonly used to implement stacks, queues, and associative arrays.

Linked lists can be categorized as directed graph data structures since each node points to others. Singly linked lists are acyclical, doubly linked lists are cyclical.

A less common form of linked lists is a circular linked list where the tail points back to the head rather than being a null pointer.

Some linked lists use sentinel nodes, which are "dummy" nodes that ensure the first and or last nodes still point to another. These simplify some algorithms.

### Singly linked list
![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png)

### Doubly linked list
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Doubly-linked-list.svg/610px-Doubly-linked-list.svg.png)

## Complexity

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 

In order to access an item or search the list, you must traverse the whole thing. In order to insert or delete nodes, you only need to move the position of pointers.

## Singly Linked List
```java
public class Node<Object> {
    private Node next;
    private Object data;

    public Node(Object data) {
        this.next = null;
        this.data = data;
    }
    public Node(Object data, Node next) {
        this.next = next;
        this.data = data;
    }
    public Object getData() {
        return data;
    }
    public void setData(Object data) {
        this.data = data;
    }
    public Node getNext() {
        return next;
    }
    public void setNext(Node next) {
        this.next = next;
    }
}

public class SinglyLinkedList<Node>{
    private Node head;
    private int length;

    public SinglyLinkedList() {
        head = null;
        length = 0;
    }
    public void add(Object data) {
        add(data, length);
    }
    public void add(Object data, int index) {
        Node newNode = new Node(data);
        Node current = head;

        if (head === null) {
            head = newNode;
            length++;
            return;
        }

        if (current !== null && index > 0 && index <= length) {
            for (int i = 0; i < index && current.getNext() !== null; i++) {
                current = current.getNext();
            }
        }
        newNode.setNext(current.getNext());
        current.setNext(newNode);
        length++;
    }
    public boolean remove(int index) {
        if (index < 1 || index > length || head === null) {
            return null;
        } else if (index === 0 && head !== null) {
            head = head.getNext();
            return true;
        }
        Node current = head;
        Node prev = null;
        for (int i = 0; i < index; i++) {
            if (current.getNext() !== null) {
                prev = current;
                current = current.getNext();
            } else {
                return false;
            }
        }
        prev.setNext(current.getNext());
        list--;

        return true;
    }
    public int search(Object data) {
        Node current;
        if (head !== null && data instanceof Object) {
            current = head.getNext();
            for (int i = 0; i < length; i++) {
                if (current.getData === data) {
                    return i;
                }
            }
        }
        return null;
    }
}

```

## Doubly Linked List
```java
public class Node<Object> {
    private Node next;
    private Node prev;
    private Object data;

    public Node(Object val) {
        this.next = null;
        this.prev = null;
        this.data = val;
    }
    public Node(Object data, Node next, Node prev) {
        this.next = next;
        this.prev = prev;
        this.data = data;
    }
    public Object getData() {
        return data;
    }
    public void setData(Object data) {
        this.data = data;
    }
    public Node getNext() {
        return next;
    }
    public void setNext(Node next) {
        this.next = next;
    }
    public Node getPrev() {
        return prev;
    }
    public void setPrev(Node prev) {
        this.prev = prev;
    }
}

public class DoublyLinkedList<Node> {
    private int length;
    private Node head;
    private Node tail;

    public DoublyLinkedList() {
        length = 0;
        head = null;
        tail = null;
    }
    public add(Object data) {
        add(data, length);
    }
    public add(Object data, int index) {
        Node newNode = new Node(data);
        Node current = head;

        if (head === null) {
            head = newNode;
            length++;
            return;
        }

        if (current !== null && index > 0 && index <= length) {
            for (int i = 0; i < index && current.getNext() !== null; i++) {
                current = current.getNext();
            }
        }
        newNode.setNext(current.getNext());
        current.setNext(newNode);
        newNode.setPrev(current);

        if (newNode.getNext() === null) {
            tail = newNode;
        }
        length++;
    }
    public boolean remove(int index) {
        if (index < 0 || index > length || head === null) {
            return false;
        }
        Node current = head;
        for (int i = 0; i < index; i++) {
            if (current.getNext() !== null) {
                current = current.getNext();
            } else {
                return false;
            }
        }
        Node prev = current.getPrev();
        Node next = current.getNext();
        prev.setNext(next);
        next.setPrev(prev);
        length--;
        return true;
    }
    public int search(Object data) {
        if (head !== null && data instance of Object) {
            Node current = head;
            for (int i = 0; i < length; i++) {
                
            }
        }
    }
}
```

## Practice Problems
* [Check to see if a linked list has a cycle](https://www.hackerrank.com/challenges/ctci-linked-list-cycle)
* [Find the Nth to last node in a linked list](https://www.udemy.com/python-for-data-structures-algorithms-and-interviews/learn/v4/overview)
