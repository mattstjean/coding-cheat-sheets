# Arrays

## About
Arrays are collections of elements that can be identified by an index. They are used to implement a ton of other data structures -- like queues, stacks, lists, and sometimes strings.

The Deque is a double-ended queue, extending the Queue interface. To implement a LIFO (Last-In-First-Out) stack in Java, use a deque instead of the Stack class. It is likely to be faster.

The vector is a growable and shrinkable (dynamic) array. Similar to ArrayList but are synchronized and not in the Collection framework. Don't use it in a non-thread environment because it is synchronized - poor performance adding, searching, deleting, updating. Useful if you don't know the size of your array in advance or need one that changes during its life.

The queue has elements inserted at the end and elements removed from the beginning.Is is an ordered sequence of objects but its intended to be used differently than a List. LinkedList is a standard queue implementation and store elements internally in standard LinkedList fashion allowing easy/quick insertion at tail and removal at head. PriorityQueue stores elements internally according to natural order (if they implement Comparable) or according to a Comparator passed to the PriorityQueue.

The stack is just a classical stack structure. You can push elements to the top and pop them again, ie read and remove elements from the top of the stack. It implements the List interface, but you'd rarely use it as a List. It is a subclass of Vector which is synchronized. It is recommended to use a Java Deque instead.

The set is a collection of objects where each object is unique. An object cannot occur more than once in a Java Set. The elements in a Set have no guaranteed internal order.

```Java
// Array
String[] names = {"John", "Jacob", "Smith"};
int[] nums = {10, 20, 30, 40};

// ArrayList
ArrayList<String> names = new ArrayList<String>();
names.add("John");
names.add("Jacob");
names.add("Smith");

names.get(0); // John

names.set(0, "Johnathon");

names.remove(0);
names.clear();
names.size();

for (String name : names) {
    System.out.print(" " + name);
}

Collections.sort(names);

Iterator it = names.iterator();
while (it.hasNext()) {
    System.out.print(" " + it.next());
}

// LinkedList
LinkedList<String> names = new LinkedList<String>();
names.add("John");
names.add("Jacob");
names.add("Smith");

names.get(0);

names.set(0, "Johnathon");

names.remove(0);

// ArrayDeque
ArrayDeque<String> names = new ArrayDeque<>();

names.add("John");
names.add("Jacob");
names.add("Smith");

names.addFirst("Mike");
names.addLast("Ali");

names.offer("Mark"); // insert at end
names.offerFirst("Mary"); // insert at beginning
names.offerLast("Mildred"); // insert at the end

names.getFirst();
names.getLast();

names.peek(); // first elements
names.peekFirst();
names.peekLast();

names.poll(); // return and remove first element
names.pollFirst();
names.pollLast();

names.pop(); // return and remove last element

Iterator<String> it = names.iterator();
while (it.hasNext()) {
    System.out.print(" " + it.next());
}

// Vector
Vector v = new Vector(3, 2); // Size 3, increment 2
v.size();
v.capacity();

v.addElement(new Integer(1));
v.contains(new Integer(1));

Enumeration vEnum = v.elements();
while (vEnum.hasMoreElements()) {
    System.out.print(" " + vEnum.nextElement());
}

//Queue
Queue queueA = new LinkedList();
Queue queueB = new PriorityQueue();

queueA.remove();

for(Object obj : queueA) {
    System.out.print(" " + obj.value);
}

queueA.add("A");
queueA.offer("B");

queueA.poll();
queueB.remove();

queue.contains("B");

// Set
Set setA = new HashSet();
Set setB = new LinkedHashSet();
Set setC = new TreeSet();
setA.add(element);
setA.contains(element);

for (String name : set) {
    
}

```

List vs. Set

|              List             |                  Set                 |
|-------------------------------|--------------------------------------|
|Ordered Sequence               |Unordered Sequence                    |
|Allows duplicate elements      |No duplicates                         |
|Access elements by pos         |No pos access                         |
|Multiple nulls can be stored   |Null element can only be stored once  |
|Impl.: ArrayList, LinkedList   |Impl.:HashSet, LinkedHashSet          |
|       Vector, Stack           |                                      |


In most languages, indexing starts at 0. The first item in an array can be found at the index 0. Arrays can also have multiple dimensions so matrix operations commonly use them in computer science.

Arrays are stored in memory contiguously, or in one chunk of space, so the memory address of each element in the array can be computed using this formula `address = start + (cellsize * index)`. So an array with three 32-bit integer variables could be stored at addresses 2000, 2004, 2008 so then the address of an item would be 2000 + 4 * index. In many implementations of arrays, the array block of memory only stores a pointer to the item in the array rather than the item itself in order to support dynamic typing.

Arrays have a fixed size when they are created, so insertion and deletion is not natively supported. If you were able to change the size of an array during runtime, there would be no guarantee that there would be more memory in its reserved block to use.

Many high level languages take care of resizing behind the scenes by using dynamic arrays, so the user doesn't need to initialize the array with a certain size. For example, in Python, lists are initialized automatically with overfill (or additional unused slots). They resize at 4, 8, 16, 25 etc. items ([source](https://www.laurentluce.com/posts/python-list-implementation/)). From a computational perspective, this makes them less efficient but a lot more programmer friendly!

In Java, ArrayLists use a lot of memory. If you need an array that grows as you are initializing, consider using a Builder for array creation ex. IntStream, LongStream, DoubleStream, Stream ([source](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.Builder.html)). You can create a stream by generating elements individually and adding them to a builder without the copying overhead that comes from using a temporary ArrayList. Instead of copying, the builder will use multiple arrays for better performance. Another benefit to Stream.Builder is that it can deal with > 2^31 elements if you have the memory.

```Java
Builder builder = IntStream.builder();
int arraySize = new Random().nextInt();
for (int i = 0; i < arraySize; i++) {
    builder.add(i);
}
int[] array = builder.build().toArray();
```


## Complexity

|Operation|Complexity|
|---------|----------|
|Access   |O(1)      |
|Search   |O(n)      |
|Insert   |O(n)      |
|Delete   |O(n)      | 

### Explanation
* Accessing can be done using the formula `start + (cellsize * index)`
* Searching is done by iterating through the array and seeing if the value equals the item you are searching for.
* Insertion is done by recreating the array, which means that each item must be recreated.
* Deletion is done by recreating the array, which means that each item must be recreated.


## Practice Problems
* [Check to see if two strings are anagrams of one another.](https://www.udemy.com/python-for-data-structures-algorithms-and-interviews/learn/v4/overview)
* [Check to see if two strings are permutations of each other.](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [Compress a string](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [Count the differences between two strings](https://www.hackerrank.com/challenges/ctci-making-anagrams)
* [Count the positive, negative, and zero values in an array](https://www.hackerrank.com/challenges/plus-minus?h_r=next-challenge&h_v=zen)
* [Count the valleys in a hike](https://www.hackerrank.com/challenges/counting-valleys)
* [Draw a pyramid given its height](https://www.hackerrank.com/challenges/staircase?h_r=next-challenge&h_v=zen)
* [What is the number of deletions needed to make two arrays equal?](https://www.hackerrank.com/challenges/equality-in-a-array)
* [Array left rotation](https://www.hackerrank.com/challenges/ctci-array-left-rotation)
* [Find the item in an array that doesn't have a match](https://www.hackerrank.com/challenges/ctci-lonely-integer)
* [Find the diagonal difference in a matrix](https://www.hackerrank.com/challenges/diagonal-difference)
* [Find the maximum and minimum sums in an array](https://www.hackerrank.com/challenges/mini-max-sum/submissions/code/42826333)
* [Check to see if a string can be rearranged as a palindrome](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [Check to see if a string can be made from a list of substrings](https://www.hackerrank.com/challenges/password-cracker)
* [See if a word is in a list of words](https://www.hackerrank.com/challenges/ctci-ransom-note)
* [Check if a string contains only unique characters](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [Find the max subarray](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [URLify a string](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [Zero a matrix](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/098478280X)
* [Add the even numbers in the Fibonacci sequence](https://projecteuler.net/problem=2)
* [Find the largest prime factor of a number](https://projecteuler.net/problem=3)
* [Find the largest palindrome project](https://projecteuler.net/problem=4)
* [Smallest multiple](https://projecteuler.net/problem=5)
* [Smallest square difference](https://projecteuler.net/problem=6)
* [10001st prime product](https://projecteuler.net/problem=8)
* [Largest product in a grid](https://projecteuler.net/problem=11)
* [Large sum](https://projecteuler.net/problem=13)
* [Find longest Collatz sequence](https://projecteuler.net/problem=14)
* [Number letter counts](https://projecteuler.net/problem=17)
* [Maximum path sum I](https://projecteuler.net/problem=18)
* [Non-abundant sums](https://projecteuler.net/problem=23)
* [Lexicographic permutations](https://projecteuler.net/problem=24)
* [Quadratic primes](https://projecteuler.net/problem=27)
* [Number spiral diagonals](https://projecteuler.net/problem=28)
* [Pandigital products](https://projecteuler.net/problem=32)
* [Circular primes](https://projecteuler.net/problem=34)
* [Double base palindromes](https://projecteuler.net/problem=36)
* [Truncatable primes](https://projecteuler.net/problem=37)
* [Maximum path sum II](https://projecteuler.net/problem=67)
