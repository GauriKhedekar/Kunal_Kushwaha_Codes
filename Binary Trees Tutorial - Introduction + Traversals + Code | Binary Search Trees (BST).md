# Trees:-

# 🌳 Trees Data Structure –

## What Is a Tree?

* A tree consists of **nodes connected via references**
* Similar to linked list but:

  * Linked list → 1 pointer
  * Tree → 2 pointers

### Linked List Comparison

* Nodes connected linearly
* Each node points to next

### Tree Difference

* Each node points to:

  * Left child
  * Right child

---

## Binary Tree Structure

### Node Structure

```
Node {
  value
  left
  right
}
```

* `value` can be:

  * Integer
  * Object
  * Class (Human, Car, etc.)
* `left` and `right` can point to:

  * Another node
  * `null`

---

## Why Use Trees?

### 1. Time Complexity

* Insert → O(log n)
* Delete → O(log n)
* Search → O(log n)

### 2. Ordered Structure

* Especially in Binary Search Trees
* Left subtree < Root < Right subtree

### 3. Cost Efficient

* Dynamic
* No restructuring like arrays

---

## Unbalanced Binary Tree Problem

### Example

```
10
  \
   15
     \
      20
        \
         30
```

* Height becomes O(n)
* Operations degrade to O(n)

### Solution

* **Self-balancing trees**

  * AVL Trees
  * Red-Black Trees

---

## Real World Applications of Trees

* File Systems (directories)
* Databases (AVL trees)
* Networking (routing, pathfinding)
* Mathematical expressions
* Decision Trees (Machine Learning)
* Huffman Coding (Compression)
* Heaps
* Graphs (Tree is a Directed Acyclic Graph)

---

## Tree Terminologies

### Size

* Total number of nodes

### Parent & Child

* Parent → node above
* Child → node below

### Siblings

* Nodes with same parent

### Edge

* Connection between two nodes

### Leaf Node

* Node with **no children**

### Height

* Maximum number of edges from node to a leaf

### Level

* Height of root node - height of that node = Level of that node
* Root level = 0

### Ancestor & Descendant

* If path exists from A to B:

  * A = Ancestor
  * B = Descendant

### Degree:-
- of particluar node :- No. of children it has.
- of whole Binary tree :- degree of a particular Node which must be max in a whole binary tree. 

---

## Types of Binary Trees

### 1. Complete Binary Tree

* All levels filled except last
* Last level filled left to right

### 2. Full / Strict Binary Tree

* Each node has:

  * 0 children OR
  * 2 children

### 3. Perfect Binary Tree

* All internal nodes have 2 children
* All leaf nodes at same level

### 4. Height Balanced Binary Tree

* Height = O(log n)
* Examples:

  * AVL Tree
  * Red-Black Tree

### 5. Skewed Binary Tree

* Each node has only one child
* Height = O(n)
* Similar to linked list

### 6. Ordered Binary Tree

* Nodes follow some property
* Example: Binary Search Tree

---

## Properties of Binary Trees

### Property 1: Total Nodes in Perfect Binary Tree

```
Total nodes = 2^(h+1) − 1
```

### Property 2: Leaf Nodes in Perfect Binary Tree

```
Leaf nodes = 2^h
```

### Property 3: Internal Nodes

```
Internal nodes = 2^h − 1 => Total nodes - leaf nodes = 2^(h + 1) - 1 - 2^(h) = ((2)* (2^(h))) - 1 - ((1)(2 ^(h))) = > 2^(h) - 1
```

### Property 4: Minimum Levels

* For n leaves → log(n) + 1
* For n nodes → log(n + 1)

### Property 5: Strict Binary Tree Rule

```
Leaf nodes = Internal nodes + 1
```

---

## Questions Answered (As Requested)

---

### 1️⃣ Difference between Tree, Binary Tree, Binary Search Tree

| Feature      | Tree | Binary Tree | Binary Search Tree  |
| ------------ | ---- | ----------- | ------------------- |
| Max children | Any  | 2           | 2                   |
| Ordering     | None | None        | Left < Root < Right |
| Searching    | Slow | Faster      | Fastest             |

---

### 2️⃣ Leaf Nodes – Null or No Children?

* Conceptually: **Leaf nodes have no children**
* Implementation-wise:

```
left = null
right = null
```

* Node structure always exists
* References point to null

---

### 3️⃣ Skewed Tree Explanation

* Skewed tree = binary tree where every node has only one child
* Other child is set to `null`

Example (Right-skewed):

```
10
  \
   20
     \
      30
```

* It is:

  * A binary tree
  * An unbalanced tree
* Called like linked list because:

  * Height = n
  * Traversal is linear

---

### 4️⃣ Proof: Leaf Nodes = 1 + Internal Nodes (with two children)

Example:

```
        A
       / \
      B   C
     / \
    D   E
```

* Leaf nodes: D, E, C → 3
* Internal nodes with 2 children: A, B → 2

```
3 = 2 + 1
```

* Root is included if it has children

---
# 🌳 Binary Tree – Implementation 

### Two Ways to Implement a Binary Tree

#### 1️⃣ Linked Representation (Using Nodes & References)

* Same idea as **linked list**, but instead of one reference:

  * Each node has **two references** → `left` and `right`
* Objects are linked together in memory
* This is the method used in this lecture
* Most flexible and commonly used

#### 2️⃣ Sequential Representation (Using Array)

* Tree is stored **level-wise** inside an array

* Example tree values (level order):

  ```
  5, 6, 8, 9, null, 11
  ```

* Index mapping:

| Index | Value |
| ----- | ----- |
| 0     | 5     |
| 1     | 6     |
| 2     | 8     |
| 3     | 9     |
| 4     | null  |
| 5     | 11    |

* Problem:

  * Many `null` values → **wasted memory**
  * Must predefine array size

#### When Sequential Representation Is Used

* **Heap** (Complete Binary Tree)
* **Segment Tree** (Strict Binary Tree)

👉 Normal Binary Tree / Binary Search Tree → **Linked Representation** is preferred

---

## 2. Time Complexity Insight (Height of Tree)

For a full binary tree:

```
Total nodes = 2^(h+1) - 1
```

Ignoring constants:

```
2^h ≈ n
h = log₂(n)
```

So height of a balanced tree is:

```
O(log n)
```

This explains why:

* Insert
* Search
* Traversals

are efficient when the tree is balanced

---

## 3. How Recursive Insertion Works (Populate Function)

### Core Idea

* Tree is built using **recursion**
* For every node:

  1. Ask user → insert left?
  2. If yes → create left node → recurse
  3. Ask user → insert right?
  4. If yes → create right node → recurse

Each function call:

* Handles **one node**
* Makes **two recursive calls** (left & right)

---

## 4. Recursive Call Tree Example (Populate)

Input sequence:

```
Root = 15
Left of 15 → 4
Left of 4 → 8
Right of 4 → 10
Left of 10 → 2
Right of 10 → 30
Right of 15 → 4
```

### Recursive Call Flow (Simplified)

```
populate(15)
 ├─ populate(4)
 │   ├─ populate(8)
 │   └─ populate(10)
 │       ├─ populate(2)
 │       └─ populate(30)
 └─ populate(4)
```

Each call finishes only **after both left & right calls return**

---

## 5. Your Code – Fully Commented

### 📄 BinaryTree.java

```java
package Trees_1;

import java.util.Scanner;

class BinaryTree {

    public BinaryTree() {
        // Default constructor
    }

    // Node structure (Linked Representation)
    private static class Node {
        int value;      // data stored in node
        Node left;      // reference to left child
        Node right;     // reference to right child

        public Node(int value) {
            this.value = value;
        }
    }

    private Node root; // root of the tree

    // Insert elements (starts tree creation)
    public void populate(Scanner scanner){
        System.out.println("Enter the root Node: ");
        int value = scanner.nextInt();
        root = new Node(value);
        populate(scanner, root); // recursive call
    }

    // Recursive population of tree
    private void populate(Scanner scanner, Node node){

        // LEFT child
        System.out.println("Do you want to enter left of " + node.value);
        boolean left = scanner.nextBoolean();
        if(left){
            System.out.println("Enter the value of the left of " + node.value);
            int value = scanner.nextInt();
            node.left = new Node(value);
            populate(scanner, node.left); // recursion
        }

        // RIGHT child
        System.out.println("Do you want to enter right of " + node.value);
        boolean right = scanner.nextBoolean();
        if(right){
            System.out.println("Enter the value of the right of " + node.value);
            int value = scanner.nextInt();
            node.right = new Node(value);
            populate(scanner, node.right); // recursion
        }
    }

    // Simple display (Preorder style with indentation)
    public void display(){
        display(root, "");
    }

    private void display(Node node, String indent){
        if(node == null){
            return; // base condition
        }
        System.out.println(indent + node.value);
        display(node.left, indent + "\t");
        display(node.right, indent + "\t");
    }

    // Pretty tree display (rotated view)
    public void prettyDisplay(){
        prettyDisplay(root, 0);
    }

    private void prettyDisplay(Node node, int level){
        if(node == null){
            return;
        }

        // First go to right subtree
        prettyDisplay(node.right, level + 1);

        // Print current node with indentation
        if(level != 0){
            for(int i = 0; i < level - 1; i++){
                System.out.print("|\t\t");
            }
            System.out.println("|--------->" + node.value);
        } else {
            System.out.println(node.value); // root node
        }

        // Then go to left subtree
        prettyDisplay(node.left, level + 1);
    }
}
```

---

### 📄 Main.java

```java
package Trees_1;

import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        BinaryTree binaryTree = new BinaryTree();

        binaryTree.populate(scanner);
        binaryTree.display();
        binaryTree.prettyDisplay();
    }
}
o/p:-
Enter the root Node: 
15
Do you want to enter left of 15
true
Enter the value of the left of 15
4
Do you want to enter left of 4
true
Enter the value of the left of 4
8
Do you want to enter left of 8
false
Do you want to enter right of 8
false
Do you want to enter right of 4
true
Enter the value of the right of 4
10
Do you want to enter left of 10
true
Enter the value of the left of 10
2
Do you want to enter left of 2
false
Do you want to enter right of 2
false
Do you want to enter right of 10
true
Enter the value of the right of 10
30
Do you want to enter left of 30
false
Do you want to enter right of 30
false
Do you want to enter right of 15
true
Enter the value of the right of 15
4
Do you want to enter left of 4
false
Do you want to enter right of 4
false
15
	4
		8
		10
			2
			30
	4
|--------->4
15
|		|		|--------->30
|		|--------->10
|		|		|--------->2
|--------->4
|		|--------->8

```

---

## 6. Recursive Call Trees for Display Functions (With Explanation)

---

## 6.1 Recursive Call Tree for `display()`

### Function Reminder

```java
private void display(Node node, String indent){
    if(node == null){
        return;
    }
    System.out.println(indent + node.value);
    display(node.left, indent + "	");
    display(node.right, indent + "	");
}
```

---

### Traversal Type

* This function performs **Preorder Traversal**
* Order:

```
Root → Left → Right
```

---

### Example Tree Used

```
        15
       /  \
      4    4
     / \
    8  10
      /  \
     2   30
```

---

### Recursive Call Tree (display) – Landscape Binary-Tree Style

```
                            display(15)
                           /           \
                   display(4)         display(4)
                   /       \              /   \
            display(8)   display(10)   null   null
             /     \      /        \
          null   null  display(2)  display(30)
                           /   \      /    \
                        null  null  null  null
```

---

### How to Read This Tree (display)

* Each **node = one function call**
* Left child = `display(node.left)`
* Right child = `display(node.right)`
* Printing happens **at the node itself** (preorder)
* Null means **base condition hit → return immediately**

---

### Key Explanation (display)

* Each call **prints first**, then goes left, then right
* Indentation increases with depth (`	`)
* Base case: when node is `null`, function returns
* Output order directly follows the recursive call order

---

## 6.2 Recursive Call Tree for `prettyDisplay()`

### Function Reminder

```java
private void prettyDisplay(Node node, int level){
    if(node == null){
        return;
    }

    prettyDisplay(node.right, level + 1);

    if(level != 0){
        for(int i = 0; i < level - 1; i++){
            System.out.print("|		");
        }
        System.out.println("|--------->" + node.value);
    } else {
        System.out.println(node.value);
    }

    prettyDisplay(node.left, level + 1);
}
```

---

### Traversal Type

* This function performs **Reverse Inorder Traversal**
* Order:

```
Right → Root → Left
```

---

### Recursive Call Tree (prettyDisplay) – Landscape Binary-Tree Style

```
                         prettyDisplay(15)
                        /                 \
           prettyDisplay(4)            prettyDisplay(4)
           (left of 15)                (right of 15)
              /        \                 /        \
     prettyDisplay(10)  prettyDisplay(8)  null     null
        /        \
prettyDisplay(30)  prettyDisplay(2)
     /     \            /     \
   null   null        null   null
```

---

### How to Read This Tree (prettyDisplay)

* Traversal order: **Right → Root → Left**
* Right recursive call appears **higher visually**
* Root prints **after right subtree returns**
* Left subtree prints last
* This is why output looks like a rotated tree

---

### Key Explanation (prettyDisplay)

* Right subtree is printed **first**, so it appears on top
* Root is printed **after right subtree finishes**
* Left subtree printed last
* `level` controls indentation and visual tree rotation
* This makes the tree appear **sideways**

---

## 6.3 Why Outputs Look Different

| Function          | Traversal       | Visual Result      |
| ----------------- | --------------- | ------------------ |
| `display()`       | Preorder        | Top-down, indented |
| `prettyDisplay()` | Reverse Inorder | Rotated tree view  |

---

## 6.4 One-Line Intuition

* `display()` → **"Print while going down"**
* `prettyDisplay()` → **"Print while coming back"**

---

## 7. Output Explanation (Your Given Output)

### Simple Display Output

```
15
	4
		8
		10
			2
			30
	4
```

* This is **preorder traversal**
* Indentation represents depth

---

### Pretty Display Output

```
|--------->4
15
|        |        |--------->30
|        |--------->10
|        |        |--------->2
|--------->4
|        |--------->8
```

### How It Works

* Right subtree printed first
* Root printed in center
* Left subtree printed last
* Indentation = `level` depth

---

## Another example to display how pretty output in console will look like:-

### Input

```
Root = 10
Left of 10 → 5
Right of 10 → 20
Left of 5 → 3
Right of 5 → 7
```

### Pretty Output

```
|--------->20
10
|        |--------->7
|--------->5
|        |--------->3
```

---

## 8. Key Takeaways

* Binary Trees are **naturally recursive**
* Populate = DFS-style recursion
* Display = preorder traversal
* PrettyDisplay = reverse inorder traversal
* Drawing recursion trees on paper makes everything clear

---



