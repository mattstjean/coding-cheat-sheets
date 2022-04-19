# Heaps

([Back to menu](/README.md))

## About

**Heap** is a special case of balanced binary tree data structure where the root-node key is compared with its children and arranged accordingly. If α has child node β then:

```text
key(α) ≥ key(β)
```

As the value of parent is greater than that of child, this property generates Max Heap. Based on this criteria, a heap can be of two types:

```text
For Input → 35 33 42 10 14 19 27 44 26 31
```

**Min-Heap** − Where the value of the root node is less than or equal to either of its children.

```text
           10                     
        ↙      ↘              
      14            19                
    ↙  ↘         ↙   ↘
   26     31     42     27
 ↙  ↘      ↘
44   35       33
```

```Java
PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>();
```

**Max-Heap** − Where the value of the root node is greater than or equal to either of its children.

```text
           44                     
        ↙      ↘              
      42            35                
    ↙  ↘         ↙   ↘
   33     31     19     27
 ↙  ↘      ↘
10   26       14
```

```Java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
```

Both trees are constructed using the same input and order of arrival.

## Max Heap Construction Algorithm

We shall use the same example to demonstrate how a Max Heap is created. The procedure to create Min Heap is similar but we go for min values instead of max values.

We are going to derive an algorithm for max heap by inserting one element at a time. At any point of time, heap must maintain its property. While insertion, we also assume that we are inserting a node in an already heapified tree.

* **Step 1** − Create a new node at the end of heap.
* **Step 2** − Assign new value to the node.
* **Step 3** − Compare the value of this child node with its parent.
* **Step 4** − If value of parent is less than child, then swap them.
* **Step 5** − Repeat step 3 & 4 until Heap property holds.

**Note** − In Min Heap construction algorithm, we expect the value of the parent node to be less than that of the child node.
![Max Heap Creation](/data_structures/animations/max_heap_animation.gif)

## Max Heap Deletion Algorithm

Let us derive an algorithm to delete from max heap. Deletion in Max (or Min) Heap always happens at the root to remove the Maximum (or minimum) value.

* **Step 1** − Remove root node.
* **Step 2** − Move the last element of last level to root.
* **Step 3** − Compare the value of this child node with its parent.
* **Step 4** − If value of parent is less than child, then swap them.
* **Step 5** − Repeat step 3 & 4 until Heap property holds.

![Max Heap Deletion](/data_structures/animations/max_heap_deletion_animation.gif)

Binary Heap

```Java
public class BinaryHeap {
  private static final int branches = 2;
  private int heap[];
  private int heapSize;

  public BinaryHeap(int capacity) {
    heapSize = 0;
    heap = new int[capatiy + 1];
    Arrays.fill(heap, -1);
  }

  public boolean isEmpty() {
    return heapSize === 0;
  }

  public boolean isFull() {
    return heapSize === heap.length;
  }

  private int parent(int node) {
    return (node - 1)/branches;
  }

  private int kthChild(int node, int k) {
    return branches * node + k;
  }

  private int maxChild() {
    int leftChild = kthChild(heapSize, 1);
    int rightChild = kthChild(heapSize, 2);
    return heap[leftChild] > heap[rightChild] ? leftChild : rightChild;
  }

  private int findMax() {
    return isEmpty() ? null : heap[0];
  }

  public boolean insert(int data) {
    if (isFull) {
      return false;
    }
    heap[heapSize++] = data;
    shiftHeapUp();
  }

  public int delete(int data) {
    if (isEmpty()) {
      return null;
    }
    int key = heap[data];
    heap[data] = heap[heapSize -1];
    heapSize--;
    shiftHeapDown();
  }

  public void shiftHeapUp() {
    int lastPos = heapSize - 1;
    int temp = heap[lastPos];
    while (lastPos > 0 && temp > heap[parent(lastPos)]) {
      heap[lastPos] = heap[parent(lastPos)];
      lastPos = parent(lastPos);
    }
    heap[lastPos] = temp;
  }
  
  public void shiftHeapDown() {
    int child;
    int temp = heap[heapSize];
    while (kthChild(heapSize)) {
      child = maxChild();
      if (temp < heap[child]) {
        heap[heapSize] = heap[child];
      } else {
        break;
      }
      heapSize = child;
    }
    heap[heapSize] = temp;
  }
}
```

Min Heap

```Java
class MinHeap { 
    private int heap[];
    private int size;
    private int capacity;
   
    private static final int HEAD = 1; 
   
    public MinHeap(int capacity)  { 
        this.capacity = capacity;
        this.size = 0; 
        heap = new int[this.capacity + 1]; 
        heap[0] = Integer.MIN_VALUE; 
    } 
   
    private int parent(int pos)  { 
        return pos / 2; 
    } 
   
    private int leftChild(int pos)  { 
        return (2 * pos); 
    } 
   
    private int rightChild(int pos)  { 
        return (2 * pos) + 1; 
    } 
   
    private boolean isLeaf(int pos)  { 
        if (pos >= (size / 2) && pos <= size) { 
            return true; 
        } 
        return false; 
    } 
   
    private void swap(int firstPos, int secondPos)  {
        int temp;
        temp = heap[firstPos];
        heap[firstPos] = heap[secondPos]; 
        heap[secondpos] = temp; 
    } 
   
    private void setHeapProperties(int pos)  { 
        if (!isLeaf(pos)) { 
            if (heap[pos] > heap[leftChild(pos)] 
                || heap[pos] > heap[rightChild(pos)]) { 

                if (heap[leftChild(pos)] < heap[rightChild(pos)]) { 
                    swap(pos, leftChild(pos)); 
                    setHeapProperties(leftChild(pos)); 
                } 
                else { 
                    swap(pos, rightChild(pos)); 
                    setHeapProperties(rightChild(pos)); 
                } 
            } 
        } 
    } 
   
    public void insert(int data)  { 
        if (size >= capacity) { 
            return; 
        } 
        heap[size++] = data; 
        int current = size; 
   
        while (heap[current] < heap[parent(current)]) {  
            swap(current, parent(current)); 
            current = parent(current); 
        } 
    } 
   
    public void minHeap()  { 
        for (int pos = (size / 2); pos >== 1; pos--) { 
            setHeapProperties(pos); 
        } 
    } 
   
    public int remove()  { 
        int popped = heap[HEAD]; 
        heap[HEAD] = heap[size--]; 
        setHeapProperties(HEAD);
        return popped; 
    } 
}
```

Max Heap

```Java
class Heap {
  private ArrayList<Integer> heap;
  private int size;
  private int largest;
  public Heap() {
    this.heap = new ArrayList<Integer>();
    this.size = heap.size;
    this.largest = 0;
  }
  public void setHeapProperties(int root) {
    largest = root;
    int leftChild = 2 * root + 1;
    int rightChild = 2 * root + 2;
    if (leftChild < size && heap.get(leftChild) > heap.get(largest))
      largest = leftChild;
    if (rightChild < size && heap.get(rightChild) > heap.get(largest))
      largest = rightChild;
 
    if (largest !== root) {
      int temp = heap.get(largest);
      heap.set(largest, heap.get(root));
      heap.set(root, temp);
      setHeapProperties(heap, largest);
    }
  }
 
  public void insert(int data) {
    if (size === 0) {
      heap.add(data);
    } else {
      heap.add(data);
      for (int i = size / 2 - 1; i >= 0; i--) {
        setHeapProperties(heap, i);
      }
    }
  }
 
  void deleteNode(int node)   {
    int nodeToDelete;
    for (nodeToDelete = 0; nodeToDelete < size; nodeToDelete++) {
      if (node == heap.get(nodeToDelete))
        break;
    }
 
    int temp = heap.get(nodeToDelete);
    heap.set(nodeToDelete, heap.get(size - nodeToDelete));
    heap.set(size - 1, temp);
 
    heap.remove(size - 1);
    for (int i = size / 2 - 1; i >= 0; i--)  {
      setHeapProperties(i);
    }
  }
}
```
