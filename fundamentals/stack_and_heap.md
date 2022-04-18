# Stack Memory and Heap Space

## Stack Memory in Java
It is used for static memory allocation and the execution of a thread. It contains primitive values that are specific to a method and references to objects referred from the method that are in a heap.

Access is in Last-In-First-Out (LIFO) order. Whenever a new method is called, a new block is created on top of the stack which contains values specific to that method, like primitives and references to objects.

When the method finishes, its corresponding stack frame is flushed.

1. Grows and shrinks as new methods are called and returned
2. Variables inside the stack exist only as long as the method that created them is running
3. Automatically allocated and deallocated
4. If it's fully, Java will throw a StackOverFlowError
5. Access is fast compared to heap
6. Threadsafe, as each thread has its own stack

## Heap Space in Java
It is used for dynamic memory allocation of Java objects and JRE classes at runtime. New objects are always created in heap space, and references to these objects are stored in stack memory.

These objects have global access and we can access them from anywhere in the application.

We can break this memory model down into smaller parts, called generations:

- Young Generation - all new objects are allocated and aged. Minor garbage collection occurs when this is full.
- Old or Tenured Generation - long surviving objects. When objects are stored in the Young Generation, a threshold for the object's age is set, and when that threshold is reached, the object is moved to the old generation.
- Permanent Generation - this consists of JVM metadata for the runtime classes and application methods.

1. Accessed via complex memory management techniques (seen above)
2. If heap space is full, Java will throw OutOfMemoryError
3. Access is slower compared to stack
4. In contrast to stack, this memory isn't automatically deallocated. It needs garbage collector to free up unused objects to maintain memory usage efficiency
5. In contrast to stack, a heap isn't threadsafe and needs to be guarded by properly synchronizing code.
