# AVL Trees - Self Balancing Binary Search Trees

![o](images/AVL1.jpg)

-----
![o](images/AVL2.jpg)

-------
![o](images/AVL3.jpg)

-------

#### Codes:-
AVL.java
```java
package Trees_1;

public class AVL {
    public class Node {
        private int value;
        private Node left;
        private Node right;
        private int height;

        public Node(int value) {
            this.value = value;
        }

        public int getValue() {
            return value;
        }
    }

    private Node root;

    public AVL() {
    }

    public int height() {
        return height(root);
    }

    private int height(Node node) {
        if (node == null) {
            return -1;
        }
        return node.height;
    }

    public boolean isEmpty() {
        return root == null;
    }

    public void insert(int value) {
        this.root = insert(value, root);
    }

    private Node insert(int value, Node node) {
        if (node == null) {
            node = new Node(value);
            return node;
        }

        if (value < node.value) {
            node.left = insert(value, node.left);
        }

        if (value > node.value) {
            node.right = insert(value, node.right);
        }

        // UPDATED: Correct height calculation (max of children + 1)
        // Correct? Yes. If leaf node: max(-1, -1) + 1 = 0.
        node.height = Math.max(height(node.left), height(node.right)) + 1;

        return rotate(node);
    }

    private Node rotate(Node node) {
        // it will return the original tree itself if adding a new element isn't making tree unbalanced 
        // i.e. when difference between height of left node and right node is between 1 and -1 => [1, -1]
        // that's why we are not doing any action on inserted node and above nodes if ht difference is -1, 0, or 1.
        
        if (height(node.left) - height(node.right) > 1) {
            // Left heavy
            if (height(node.left.left) - height(node.left.right) >= 0) {
                // left - left case (i.e. both child and grandchild are on the same side.)
                return rightRotate(node);
            }
            if (height(node.left.left) - height(node.left.right) < 0) {
                // left - right case (i.e. both child and grandchild are on the opposite side.)
                // first left rotate node.left i.e. left rotate child
                node.left = leftRotate(node.left);
                return rightRotate(node);
            }
        }

        if (height(node.left) - height(node.right) < -1) {
            // Right heavy
            if (height(node.right.right) - height(node.right.left) >= 0) {
                // right - right case (i.e. both child and grandchild are on the same side.)
                return leftRotate(node);
            }
            if (height(node.right.right) - height(node.right.left) < 0) {
                // right - left case (i.e. both child and grandchild are on the opposite side.)
                // FIXED: Rotate the right child first (node.right) to make it right-right case
                node.right = rightRotate(node.right);
                return leftRotate(node);
            }
        }

        return node;
    }

    // see General Diagram 1 -> for more understanding
    public Node rightRotate(Node p) {
        // initially (before rotation) setting names for convenience
        Node c = p.left;
        Node t = c.right;

        // After rotation
        c.right = p;
        p.left = t;

        // updated heights: update the new child (p) first, then the new root (c)
        p.height = Math.max(height(p.left), height(p.right)) + 1;
        c.height = Math.max(height(c.left), height(c.right)) + 1;

        return c; // return new root of subtree
    }

    // see General Diagram 1 -> for more understanding
    public Node leftRotate(Node c) {
        // initially (before rotation) setting names for convenience
        Node p = c.right;
        Node t = p.left;

        // After rotation
        p.left = c;
        c.right = t;

        // updated heights: update the new child (c) first, then the new root (p)
        c.height = Math.max(height(c.left), height(c.right)) + 1;
        p.height = Math.max(height(p.left), height(p.right)) + 1;

        return p; // return new root of subtree
    }

    public boolean balanced() {
        return balanced(root);
    }

    private boolean balanced(Node node) {
        if (node == null) {
            return true;
        }
        return Math.abs(height(node.left) - height(node.right)) <= 1 && balanced(node.left) && balanced(node.right);
    }

    public void populate(int[] nums) {
        for (int num : nums) {
            this.insert(num);
        }
    }

    public void populateSorted(int[] nums) {
        populateSorted(0, nums.length, nums);
    }

    // n = size of nums[]
    // T.C:- no. of elements * log2(n) per insertion = O(n log n)
    private void populateSorted(int start, int end, int[] nums) {
        if (start >= end) {
            return;
        }
        int mid = (start + end) / 2;
        this.insert(nums[mid]);
        populateSorted(start, mid, nums); // go in left hand side
        populateSorted(mid + 1, end, nums); // go in right hand side
    }

    public void display() {
        display(root, "Root Node: ");
    }

    private void display(Node node, String details) {
        if (node == null) {
            return;
        }
        System.out.println(details + node.getValue());
        display(node.left, "Left child of " + node.getValue() + " : ");
        display(node.right, "Right child of " + node.getValue() + " : ");
    }

    // Traversals:- debug/dry run using BST structure and stack to understand.
    // preOrder = N -> L -> R
    public void preOrder() {
        preOrder(root);
    }

    private void preOrder(Node node) {
        if (node == null) return;
        System.out.print(node.value + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    // inOrder = L -> N -> R
    public void inOrder() {
        inOrder(root);
    }

    private void inOrder(Node node) {
        if (node == null) return;
        inOrder(node.left);
        System.out.print(node.value + " ");
        inOrder(node.right);
    }

    // postOrder = L -> R -> N
    public void postOrder() {
        postOrder(root);
    }

    private void postOrder(Node node) {
        if (node == null) return;
        postOrder(node.left); // Leftmost Node printed first
        postOrder(node.right); // then Right Node
        System.out.print(node.value + " "); // then current Node
    }
}
```
Main.java
```java
package Trees_1;

public class Main {
    public static void main(String[] args) {
        AVL tree = new AVL();
        
        // Inserting 1000 numbers in ascending order to make the tree unbalanced.
        for (int i = 0; i < 1000; i++) {
            tree.insert(i);
        }
        
        // This will print the height of the tree
        System.out.println("Height of tree with 1000 nodes: " + tree.height());
        System.out.println("Is the tree balanced? " + tree.balanced());
    }
}

o/p:- 9

```
---


# Why is the Output Height 9?

When you insert **1,000 nodes into a standard Binary Search Tree in sorted order**, you get a **degenerate tree** (essentially a linked list) with a height of **999**.

However, an **AVL Tree implementation prevents this** through constant **self-balancing rotations**.

---

# 1. The Power of Logarithms

An **AVL tree maintains a height close to the theoretical minimum** of a perfectly balanced binary tree.

The height `h` of a balanced tree with `N` nodes is approximately:

```
h ≈ log₂(N)
```

### Calculation

```
2⁹  = 512
2¹⁰ = 1024
```

Since:

```
512 < 1000 < 1024
```

A perfectly packed tree with **1000 nodes** will have a height close to:

```
h ≈ 9
```

---

# 2. The AVL Guarantee

The **AVL Tree algorithm guarantees balance** by ensuring:

> For every node, the heights of the left and right subtrees differ by **at most 1**.

This is maintained using **tree rotations** (LL, RR, LR, RL).

### Height Formula (Worst Case)

In the **worst-case scenario** (the most unbalanced AVL tree possible), the height is bounded by:

```
h < 1.44 log₂(N + 2) − 1.328
```

For:

```
N = 1000
```

The **maximum possible height** would be approximately:

```
h ≈ 14
```

However, because you are **inserting numbers sequentially**, the tree performs **Left Rotations (RR Case)** very efficiently.

This keeps the tree **as balanced and bushy as possible**, resulting in an **optimal height close to 9**.

---

# 3. Comparison Table

| Feature | Standard BST (Sorted Input) | AVL Tree (Sorted Input) |
|-------|-----------------------------|--------------------------|
| Structure | Linear (Skewed) | Logarithmic (Balanced) |
| Height | **N − 1 = 999** | **≈ log₂ N = 9** |
| Search Time | **O(N)** – Slow | **O(log N)** – Very Fast |

---

# Key Takeaway

A **normal BST** can degrade into a **linked list** when inserting sorted data.

An **AVL Tree automatically rebalances itself**, guaranteeing:

```
Search / Insert / Delete = O(log N)
```

which keeps operations **extremely efficient even with large datasets**.

---

