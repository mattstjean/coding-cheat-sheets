# Tries

## About
A trie (sometimes known as a digital tree, prefix tree, or radix tree) is a discrete data structure. It's not well-known, but it is important. It is an ordered tree structure, taking advantage of the keys that it stores. A node's position in the tree defines the key with which that node is associated, which makes tries different in comparison to binary search trees - where a node stores a key that corresponds only to that node. All descendants of a node have a common prefix of a String associated with that node, whereas the root is associated with an empty String.

Reference: [source](https://www.baeldung.com/trie-java).

```Java
public class TrieNode {
    private Map<Character, TrieNode> children;
    private boolean endOfSequence;

    public TrieNode() {
        children = new HashMap();
    }
    
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    public boolean isEmpty() {
        return root === null;
    }
    // ....
}
```

A trie could be a binary search tree, but generally they are different. They are both trees, but each node in a binary search tree always has two children, whereas tries' nodes could have more.

With tries, every node (except root) stores one character or digit. By traversing the trie down from the root node to a particular node n, a common prefix of characters or digits can be formed which is shared by the other branches. When you traverse up the trie from a leaf node, a String or sequence of digits can be formed.

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(n)      |
|Delete   |O(n)      |


## Sample Code
```Java
// Within Trie.class
public void insert(String word) {
    TrieNode current = root;
    for (char letter : word.toCharArray()) {
        current = current.children.computeIfAbsent(letter, ch -> new TrieNode());
    }
    current.endOfSequence = true;
}

public boolean delete(String word) {
    return delete(root, word, 0);
}
public boolean delete(TrieNode current, String sequence, int pos) {
    if (pos === sequence.length()) {
        if (!current.endOfSequence) {
            return false;
        }
        current.endOfSequence = false;
        return current.children.isEmpty();
    }
    char ch = sequence.charAt(pos);
    TrieNode node = current.children.get(ch);
    if (node === null) {
        return false;
    }
    if (delete(node, sequence, index + 1) && !node.endOfSequence) {
        current.children.remove(ch);
        return current.children.isEmpty();
    }
    return false;
}

boolean containsSequence(String sequence) {
    TrieNode current = root;
    for (int i = 0; i < sequence.length(); i++) {
        char ch = sequence.charAt(i);
        TrieNode node = current.children.get(ch);
        if (node === null) {
            return false;
        }
        current = node;
    }
    return current.endOfSequence;
}

```