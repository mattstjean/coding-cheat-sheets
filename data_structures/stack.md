# Stacks

## About
Stacks are data structures (or collections) which order removal and insertion in a last in, first out (or LIFO) way. There are two operations that define a stack - push and pop. Pushing an item means adding it to the top of the stack. Popping an item means removing it from the top of the stack. Therefore, newer items are at the top and will be accessed first, older items are near the bottom and are accessed last.

![](http://legacy.earlham.edu/~ltnguyen14/cs%20web/pics/stack.png) 

Back buttons, undo functionality, and function calls in programming are usually implemented using stacks.

## Complexity

The time complexity of stack operations depends on the implementation of a stack. Some implementations use arrays or array lists, which mean that the operations have similar complexities to those of an array. Others use nodes and pointers or linked lists and therefore would have similar complexities.

## Code Example using Nodes
```Java
public class Node() {
    private Object data;
	private Node next;
	
	public Node(Object data) {
		this.data = data;
		this.next = null;
	}
	public Node(Object data, Node next) {
		this.data = data;
		this.next = next;
	}
}

public class Stack() {
	private Node head;
	
	public Stack(Object object) {
		this.head = new Node(object, null);
	}

	public Stack push(Object data) {
		head = new Node(data, head);
	}
	public Object pop() {
		Object data = head.data;
		head = head.next;
		return data;
	}
	public Object peek() {
		return head.data;
	}
}
```
In the above example, the big-O complexity looks like:

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      |

In order to access an item or search for one we would have to traverse the linked list. Inserting an item will always happen from the top, so it will always happen in constant time.


## Code Example using an Array
```Java
public class Stack {
	private int storage[];
	private int top;
	private int capacity;

	public Stack(int size) {
		storage = new int[size];
		capacity = size;
		top = -1;
	}

	public boolean push(int data) {
		if (isFull()) {
			return false;
		}
		storage[top++] = data;
	}
	public int pop() {
		if (isEmpty()) {
			return null;
		}
		return storage[top--];
	}
	public int peek() {
		if (isEmpty()) {
			return null;
		}
		return storage[top];
	}
	public Boolean isFull() {
		return top === capacity - 1;
	}
	public Boolean isEmpty() {
		return top === -1;
	}
}
```
In the above example, the big-O complexity looks like:

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      |

In order to access an item or search for one we would have to traverse the linked list. Inserting an item will always happen from the top, so it will always happen in constant time. Python [optimizes](https://www.ics.uci.edu/~pattis/ICS-33/lectures/complexitypython.txt) append and pop if they are at the end of a list, so the operations also happen in constant time. Some other implementations of arrays would not have similar optimizations and would then have insertion and deletion at O(n).

## Practice Problems

* [Implement a queue using two stacks](https://www.hackerrank.com/challenges/ctci-queue-using-two-stacks)
* [Check to see if a sequence of parentheses is balanced](https://www.hackerrank.com/challenges/ctci-balanced-brackets)
