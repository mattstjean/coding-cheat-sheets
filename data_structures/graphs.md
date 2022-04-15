# Graphs

## About

Graphs are non-linear data structures that can show any type of relationship. Many data structures fall under the parent category of graphs -- like linked lists and trees. Graphs have nodes (also called vertices) and edges. The node holds the data and then the edges point to related nodes. There are two types of edges: directed and undirected. Directed edges point in a direction whereas undirected edges point both ways. 

Good examples of graphs in use are Facebook friends, Twitter following (which would be directed), or a map of Metro stops.

There are many ways to store a graph data structure. You can use pointers and nodes, or you could use an adjacency list or matrix.


## Example Graph
```
     A –→ B ←–––– C → D ↔ E
     ↑    ↕     ↙ ↑     ↘
     F –→ G → H ← I ––––→ J
           ↓     ↘ ↑
           K       L
```
Image from [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures/blob/master/itsy-bitsy-data-structures.js).

## Glossary

* **Edges** - connections between nodes.
* **Directed** - edges point in a direction.
* **Undirected** - edges point in both directions.
* **Euler Path** - path that visits each edge just once. A graph must have either zero or two vertices with an odd degree to have an euler path. 
* **cycle** - circle made of edges.

## Sample Code - Implementation with Adjacency List
```Java
public class Edge {
      private int src;
      private int dest;
      private int weight;
      public Edge(int src, int dest, int weight) {
            this.src = src;
            this.dest = dest;
            this.weight = weight;
      }
}
public class Node {
      private int value;
      private int weight;
      public Node(int value) {
            this.value = value;
            this.weight = null;
      }
      public Node(int value, int weight) {
            this.value = value;
            this.weight = weight;
      }
}
public class Graph {
      private LinkedList<Integer> adjacencyList[];
      private int vertices;
      public Graph(int vertices) {
            this.vertices = vertices;
            adjacencyList = new LinkedList[vertices];
            for (int i = 0; i < vertices; i++) {
                  adjacencyList[i] = new LinkedList();
            }
      }
      public void addEdge(int src, int dest) {
            adjacencyList[src].add(dest);
      }
}
```

You can traverse a graph using: Depth-first traversal and Breadth-first traversal.

For depth-first traversal, you start with the root node and insert it into the stack, you pop the item from the stack and insert it into the "visited" list, for a node marked as "visited" (ie in visited list) add the adjacent nodes of this node that are not yet marked visited, to the stack. Repeat until the stack is empty.

```java
public void depthFirstTraversal(int vertex, boolean visited[]) {
      visited[vertex] = true;
      Iterator<Integer> it = adjacencyList[vertex].listIterator();
      while (it.hasNext()) {
            int next = it.next();
            if (!visited[next]) {
                  depthFirstTraversal(next, visited);
            }
      }
}
public void depthFirstTraversal(int vertex) {
      boolean visited[] = new boolean[vertices];
      depthFirstTraversal(vertex, visited);
}
```

For breadth-first traversal, you use a queue to store the nodes. Start with the root node and insert it into your queue. Then for each node: remove the root node from the queue and add it to the visited list, then add all adjacent nodes of the root node to the queue. Repeat this for each of those adjacent nodes.

```java
public void breadthFirstTraversal(int vertex) {
      boolean visited[] = new boolean[vertices];
      LinkedList<Integer> queue = new LinkedList<Integer>();
      visited[vertex] = true;
      queue.add(vertex);

      while (queue.size() !== 0) {
            vertex = queue.poll();
            
            Iterator<Integer> it = adjacencyList[vertex].listIterator();
            while (it.hasNext()) {
                  int next = it.next();
                  if (!visited[next]) {
                        visited[next] = true;
                        queue.add(next);
                  }
            }
      }
}
```
