# Trees

([Back to menu](/README.md))

## About

Trees are graph data structures that are hierarchical and unidirectional. They have a root value, and then sub-trees of children that each have parents. They are represented as a series of linked nodes. Each node has a value and then pointers to its children.

Trees have nodes and vertices without any cycles. They are also directed - the parents point down to the children rather than having bidirectional relationships.

The most common tree is a binary tree - where where every node has at most two children.

Java sample code created using [source](https://www.baeldung.com/java-binary-tree).

## Sample Code

```Java
public class Node {
    private int value;
    Node left;
    Node right;

    public Node(int value) {
        this.value = value;
        this.right = null;
        this.left = null;
    }

    public Node(int value, Node left, Node right) {
        this. value = value;
        this.right = right;
        this.left = left;
    }
}

public class BinaryTree {
    private Node root;
}
```

## Glossary

* **Root** - the top node of the tree.
* **Child** - a node below the parent.
* **Parent** - a node above a child. Note - a node can be both a parent and a child!
* **Siblings** - nodes with the same parent.
* **Leaf** - a node with no children.
* **Branch** - a node with a child.
* **Edge** - Connection between nodes.

## Tree Visual

```text
          A                     
        ↙   ↘              
      B       C                
    ↙  ↘
   D    E
```

## Common Operations

* **Searching** - Searching a binary search tree for a specific key can be programmed recursively or iteratively.

## Recursive Search

```Java
public Node searchRecursively(Node current, int value) {
    if (current === null) {
        return null;
    }
    if (value === current.value) {
        return node;
    }
    if (value < current.value) {
        searchNodeRecursively(current.left, value);
    } else {
        searchNodeRecursively(current.right, value);
    }
}
```

## Iteratively

```Java
public Node searchIteratively(Node current, int value) {
    while (current !== null) {
        if (value === current.value) {
            return current;
        }
        if (value < current.value) {
            current = current.left;
        } else if (value > current.value) {
            current = current.right;
        }
    }
    return null;
}
```

* **Insertion** - Insertion begins as a search would begin; if the key is not equal to that of the root, we search the left or right subtrees as before. Eventually, we will reach an external node and add the new key-value pair (here encoded as a record 'newNode') as its right or left child, depending on the node's key. In other words, we examine the root and recursively insert the new node to the left subtree if its key is less than that of the root, or the right subtree if its key is greater than or equal to the root.

```Java
public BinaryTree insert(node, value) {
    if (node === null) {
        return new Node(value);
    }
    if (value === node.value) {
        return new Node(value, left, right);
    }
    if (value < node.value) {
        return new Node(insert(node.left, value), node.value, node.right);
    }
    return new Node(node.left, node.value, insert(node.right, value));
}
```

* **Deletion** - When removing a node from a binary search tree it is mandatory to maintain the in-order sequence of the nodes.

```Java
private int findSmallestValue(Node node) {
    Node current = node;
    while (current.left !== null) {
        current = current.left;
    }
    return current;
}

private Node delete(int value) {
    root = delete(root, value);
}

private Node delete(Node node, int value) {
    Node current = node;
    if (current === null) {
        return null;
    }
    if (value === current.value) {
        // Leaf node, ie no children
        if (current.left === null && current.right === null) {
            return null;
        }
        // One child, left.
        if (current.right === null) {
            return current.left);
        }
        // One child, right.
        if (current.left === null) {
            return current.right;
        }
        // Two children - reorganize
        int smallestValue = findSmallestValue(node);
        current.value = smallestValue;
        current.right = delete(current.right, smallestValue);
        return current;
    }
    if (value < current.value) {
        current.left = delete(current.left, value);
        return current;
    }
    current.right = delete(current.right, value);
}
```

* **Traversal** - Once the binary search tree has been created, its elements can be retrieved in-order by recursively traversing the left subtree of the root node, accessing the node itself, then recursively traversing the right subtree of the node, continuing this pattern with each node in the tree as it's recursively accessed. As with all binary trees, one may conduct a pre-order traversal or a post-order traversal, but neither are likely to be useful for binary search trees. An in-order traversal of a binary search tree will always result in a sorted list of node items (numbers, strings or other comparable items).

```text
          6                     
        ↙   ↘              
      4       8
    ↙  ↘     ↙  ↘
   3    5   7    9
```

Depth-First Search goes as deep as possible in every child before exploring the next sibling: in-order, pre-order, post-order.

```Java
public void traverseInOrder(Node node) {
    // 3 4 5 6 7 8 9
    if (node !== null) {
        traverseInOrder(node.left);
        System.out.print(" " + node.value);
        traverseInOrder(node.right);
    }
}

public void traversePreOrder(Node node) {
    // 6 4 3 5 8 7 9
    if (node !== null) {
        System.out.print(" " + node.value);
        traversePreOrder(node.left);
        traversePreOrder(node.right);
    }
}

public void traversePostOrder(Node node) {
    // 3 5 4 7 9 8 6
    if (node !== null) {
        traversePostOrder(node.left);
        traversePostOrder(node.right);
        System.out.print(" " + node.value);
    }
}
```

Breadth-First Search visits all nodes of a level before going to the next level: level-order.

```Java
public void traverseLevelOrder() {
    // 6 4 8 3 5 7 9
    if (root === null) {
        return;
    }
    Queue<Node> nodes = new LinkedList<>();
    nodes.add(root);

    while (!nodes.isEmpty()) {
        Node node = nodes.remove();
        System.out.print(" " + node.value);
        if (nodes.left !== null) {
            nodes.add(node.left);
        }
        if (node.right !== null) {
            nodes.add(node.right);
        }
    }
}
```
