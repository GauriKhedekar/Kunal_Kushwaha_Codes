# Trees:-

![q](images/BT1.png)
![q](images/BT2.png)
![q](images/BT3.png)
![q](images/BT4.png)
![q](images/BT5.png)
![q](images/BT6.png)

---

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

![i](

# 🌳 Binary Search Trees (BST)

![q](images/BST1.png)
![q](images/BST2.png)

---


### 1️⃣ What is a Binary Search Tree?

A Binary Search Tree (BST) is a type of binary tree where:

Left subtree → contains smaller elements

Right subtree → contains greater elements

This rule applies to every node

----


### ⚖️ Balanced Binary Tree
Definition

A tree is balanced if:

The height difference between the left and right child of any node is ≤ 1

Height Difference Rule:

`|height(left) - height(right)| ≤ 1`

```
| Left Height | Right Height | Difference | Balanced?  |
| ----------- | ------------ | ---------- | ---------  |
| 0           | 0            | 0          | ✅ Yes     |
| 1           | 0            | 1          | ✅ Yes     |
| 2           | 0            | 2          | ❌ No      |
```

---

### 🌲 Why Balance Matters?

If tree is balanced:

- Maximum height = log n

- Operations become O(log n)

If not balanced:

- Tree becomes like a linked list

- Operations become O(n)

---

### ⏱️ Time Complexity in Balanced BST

For balanced BST:

- Insertion → O(log n)

- Deletion → O(log n)

- Search → O(log n)

Why?

Because:

- At every level → only 1 comparison

- Total levels in balanced tree = log n

- So total comparisons = log n

---

### 🌳 BST Insertion Logic
Example Insertions

Insert in order:

```
Insert 15 → becomes root
Insert 10 → 10 < 15 → goes left
Insert 5 → 5 < 15 → left → 5 < 10 → left
Insert 20 → 20 > 15 → right
Insert 12 → 12 < 15 → left → 12 > 10 → right
```

### 🔁 Important Concept

At each level:

- Compare with only one node

Decide:

- Go left

- OR go right

- Never compare multiple nodes at same level

---

### 📦 Node Structure (Java Concept)

Each node contains:

```
int value
Node left
Node right
int height
```

Height is stored to:

- Quickly calculate balance

- Avoid recalculating height every time

---


### 📏 Height Function

```
if (node == null) return -1
else return node.height
```

---


### 🌲 Is Tree Empty?

```
return root == null
```

---


### 🔁 Recursive Insert Function Logic


Base Case:

- If node is null:

- Create new node

- Return it

- Recursive Case:

- If value < node.value:

'node.left = insert(value, node.left)'

- If value > node.value:

'node.right = insert(value, node.right)'
  
##### After insertion:

Update height:

'node.height=max(height(left),height(right))+1'

---

### 🔄 How Recursive Insert Works (Example Insert 8)


Tree:

```
        15
       /
      10
     /
    5
```

Insert 8:

- 8 < 15 → left

- 8 < 10 → left

- 8 > 5 → right

- Right is null → create node 8

Then:

- 5.right = 8

- Update height of 5

- Update height of 10

- Update height of 15

- Heights updated while recursion returns upward.

---


### ⚖️ Check If Tree is Balanced


Logic:

```
return (
  |height(left) - height(right)| <= 1
  AND balanced(left)
  AND balanced(right)
)
```

Base Case:

'if node == null → return true'

---


### 📺 Display Function Logic


Recursive display:

```
display(node):
    if node == null → return
    print details + node.value
    display(node.left)
    display(node.right)
```

Used to print:

```
Root node

Left child of X

Right child of X
```

---


### 📥 Populate Multiple Elements

Instead of inserting one by one manually:

```
for each element in array:
    insert(element)
```

---


### ⚠️ Problem with Sorted Array Insertion

If array is sorted:

`1 2 3 4 5 6 7`

Tree becomes:

```
1
 \
  2
   \
    3
     \
      4
```

- This is skewed → becomes O(n)


---


### ✅ Solution for Sorted Array


Use Middle Element Strategy

- Given:

`1 2 3 4 5 6 7 8 9 10`

Step 1:

- Take middle → 5 → root

Step 2:

- Left half → 1 2 3 4
- Right half → 6 7 8 9 10

Step 3:

- Recursively repeat:

- Middle of left → 2

- Middle of right → 8

- Continue

- This builds a balanced tree.


---


### Recursive Function:

```
populateSorted(arr, start, end):
    if start >= end → return

    mid = (start + end)/2
    insert(arr[mid])

    populateSorted(arr, start, mid)
    populateSorted(arr, mid+1, end)
```

---


### Time Complexity

- Insert called n times

- Each insert takes log n

- Total = O(n log n)

---


### 🌲 Tree Traversals


#### 1️⃣ Preorder Traversal

Order:
- Node → Left → Right
- Example:

- Tree:

```
      10
     /  \
    20   12
   / \
 15  13
```

- Preorder:

`10 20 15 13 12`

When to Use?

- Copying tree

- Serializing tree

- Expression tree evaluation

- Making duplicate tree


---


#### 2️⃣ Inorder Traversal


Order:
- Left → Node → Right
- Example (same tree):
  
`15 20 13 10 12`

##### 🔥 Most Important Use Case

- In a Binary Search Tree, inorder traversal prints: Elements in sorted order

- Example BST:

```
        5
       / \
      3   7
     / \
    2   4
```

- Inorder Output:

`2 3 4 5 7`

- Because:

- Leftmost node is smallest

- Then move upward

---


### 3️⃣ Postorder Traversal

- Order:

- Left → Right → Node

- Example (same tree):

- Tree:

```
      10
     /  \
    20   12
   / \
 15  13
```

- Postorder:

`15 13 20 12 10`

- When to Use?

- Deleting tree

- Freeing memory

- Expression tree evaluation (postfix)

- Processing children before parent

---


### 🧠 Important Concept

- Traversal always works recursively:

- Process part of tree

- Call same function on subtrees

- Recursion handles stack


---


### 🧩 Formula Used Earlier

Total nodes in complete binary tree:

`𝑛 = 2^(ℎ + 1) − 1`

Where:

- n = number of nodes

- h = height

So,

`h=log(n)`

- That’s why balanced BST operations are O(log n).


---


### 📌 Summary


```
| Concept          | Key Point                      |
| ---------------- | ------------------------------ |
| Balanced Tree    | Height difference ≤ 1          |
| BST Property     | Left < Node < Right            |
| Search           | O(log n)                       |
| Insert           | O(log n)                       |
| Sorted Array Fix | Use middle element recursively |
| Preorder         | Node → Left → Right            |
| Inorder          | Left → Node → Right            |
| Inorder in BST   | Sorted Output                  |
```

---

### Codes:-


✅ BinarySearchTree.java

```java
package Trees_1;

/*
    Binary Search Tree (BST)

    Properties:
    1. Left subtree values < Node value
    2. Right subtree values > Node value
    3. No duplicate values (in this implementation)

    This implementation also maintains height of each node.
*/

public class BinarySearchTree {

    // Node class represents each element in the tree
    public class Node {
        private int value;      // Value stored in node
        private Node left;      // Reference to left child
        private Node right;     // Reference to right child
        private int height;     // Height of node (for balance checking)

        public Node(int value) {
            this.value = value;
        }

        public int getValue() {
            return value;
        }
    }

    private Node root; // Root node of BST

    // Constructor
    public BinarySearchTree() {
    }

    /*
        Returns height of a given node.
        If node is null, height is -1.
        (Because leaf node height = 0)
    */
    public int height(Node node) {
        if (node == null) {
            return -1;
        }
        return node.height;
    }

    // Checks whether tree is empty
    public boolean isEmpty() {
        return root == null;
    }

    /*
        Public insert method.
        Calls private recursive insert function.
    */
    public void insert(int value) {
        root = insert(value, root);
    }

    /*
        Recursive insertion logic:

        1. If node is null → create new node.
        2. If value < node.value → go to left subtree.
        3. If value > node.value → go to right subtree.
        4. Update height after insertion.
    */
    private Node insert(int value, Node node) {

        // Base condition: create new node
        if (node == null) {
            return new Node(value);
        }

        // Insert in left subtree
        if (value < node.value) {
            node.left = insert(value, node.left);
        }

        // Insert in right subtree
        else if (value > node.value) {
            node.right = insert(value, node.right);
        }

        // Update height after insertion
        node.height = Math.max(height(node.left), height(node.right)) + 1;

        return node;
    }

    /*
        Checks if tree is height-balanced.

        A tree is balanced if:
        | height(left) - height(right) | <= 1
        for every node.
    */
    public boolean balanced() {
        return balanced(root);
    }

    private boolean balanced(Node node) {
        if (node == null) {
            return true;
        }

        return Math.abs(height(node.left) - height(node.right)) <= 1
                && balanced(node.left)
                && balanced(node.right);
    }

    /*
        Inserts elements from array one by one.
        Time Complexity:
        Worst case → O(n^2)
        Average case → O(n log n)
    */
    public void populate(int[] nums) {
        for (int num : nums) {
            insert(num);
        }
    }

    /*
        Creates balanced BST from sorted array.
        Picks middle element first.

        Time Complexity → O(n log n)
    */
    public void populateSorted(int[] nums) {
        populateSorted(0, nums.length, nums);
    }

    private void populateSorted(int start, int end, int[] nums) {

        if (start >= end) {
            return;
        }

        int mid = (start + end) / 2;

        // Insert middle element
        insert(nums[mid]);

        // Recursively build left subtree
        populateSorted(start, mid, nums);

        // Recursively build right subtree
        populateSorted(mid + 1, end, nums);
    }

    /*
        Display tree structure
        Shows parent-child relationship
    */
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

    // ================== TREE TRAVERSALS ==================

    /*
        PREORDER Traversal (N → L → R)
        Node → Left → Right
    */
    public void preOrder() {
        preOrder(root);
    }

    private void preOrder(Node node) {
        if (node == null) {
            return;
        }

        System.out.println(node.value);
        preOrder(node.left);
        preOrder(node.right);
    }

    /*
        INORDER Traversal (L → N → R)
        Left → Node → Right

        IMPORTANT:
        In BST, Inorder traversal gives sorted output.
    */
    public void inOrder() {
        inOrder(root);
    }

    private void inOrder(Node node) {
        if (node == null) {
            return;
        }

        inOrder(node.left);
        System.out.println(node.value);
        inOrder(node.right);
    }

    /*
        POSTORDER Traversal (L → R → N)
        Left → Right → Node
    */
    public void postOrder() {
        postOrder(root);
    }

    private void postOrder(Node node) {
        if (node == null) {
            return;
        }

        postOrder(node.left);
        postOrder(node.right);
        System.out.println(node.value);
    }
}
```

✅ Main.java


```java
package Trees_1;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        // Create BST object
        BinarySearchTree BST = new BinarySearchTree();

        // Input array
        int[] nums = {5, 2, 7, 1, 4, 6, 9, 8, 3, 10};

        // Insert elements into BST
        BST.populate(nums);

        // Display tree structure
        BST.display();

        /*
            Output structure:

            Root Node: 5
            Left child of 5 : 2
            Left child of 2 : 1
            Right child of 2 : 4
            Left child of 4 : 3
            Right child of 5 : 7
            Left child of 7 : 6
            Right child of 7 : 9
            Left child of 9 : 8
            Right child of 9 : 10
        */
    }
}
```

# My Doubts:-

### 🌳 Example BST We’ll Use

Let’s build this BST using insert:

Insert order: 5, 2, 7, 1, 4

Final Tree:

```
        5
       / \
      2   7
     / \
    1   4
```


Heights (leaf = 0, null = -1):

```
        5 (h=2)
       /       \
   2 (h=1)     7 (h=0)
    /    \
1 (0)   4 (0)
```

### 1️⃣ Stack Execution of BST.insert(4)

- Assume tree already has: 5, 2, 7, 1

- We now call:

- insert(4)


### 🔹 Recursive Call Stack


| Step | Function Call     | Comparison | Action        |
|------|-------------------|------------|--------------|
| 1    | insert(4, 5)      | 4 < 5      | Go left      |
| 2    | insert(4, 2)      | 4 > 2      | Go right     |
| 3    | insert(4, null)   | null       | Create node(4) |



### 🔹 Stack Diagram (Top = current)


```
insert(4, 5)  
    ↓  
insert(4, 2)  
    ↓  
insert(4, null)   ← base case  
```

- Now stack unwinds:

🔹 Returning Back (Very Important!)

```
insert(4, null)  
→ creates node(4)  
→ returns node(4)  
```
```
Back to insert(4, 2)  
→ node.right = returned node(4)  
→ update height of 2  
→ return node(2)  
```
```
Back to insert(4, 5)  
→ node.left = returned node(2)  
→ update height of 5  
→ return node(5)  
```

🔹 Height Updates While Unwinding
```
Node 4 → height = 0  
```
```
Node 2:  
left = 1 (h=0)  
right = 4 (h=0)  
height = max(0,0)+1 = 1  
```
```
Node 5:  
left = 2 (h=1)  
right = 7 (h=0)  
height = max(1,0)+1 = 2  
```

2️⃣ How balanced() Works (With Stack + Heights)

Your balanced condition:

```
abs(height(left) - height(right)) <= 1  
AND  
balanced(left)  
AND  
balanced(right)  
```

🔹 Start at root (5)

Heights:

```
Left height = 1  
Right height = 0  
Difference = 1 ✅  
```

Now recursive calls begin.

🔹 Stack Execution

```
balanced(5)  
    ↓  
balanced(2)  
    ↓  
balanced(1)  
```

- Step-by-Step

🔹 balanced(1)

```
left = null (-1)  
right = null (-1)  
difference = 0 ✅  
returns true  
```

🔹 balanced(4)

```
Same as above → returns true  
```

🔹 balanced(2)

```
left = 1 (0)  
right = 4 (0)  
diff = 0 ✅  
left subtree balanced = true  
right subtree balanced = true  
returns true  
```

🔹 balanced(7)

```
Leaf → true  
```

🔹 balanced(5)

```
left height = 1  
right height = 0  
diff = 1 ✅  
left balanced = true  
right balanced = true  
returns true  
```

✅ Final Answer: Tree is Balanced  

---

### Time Complexity

🔹 populate(int[] nums)

- This simply does:

```
for each element:  
    insert(element)  
```

If tree is balanced:

- Each insert = O(log n)  

- n inserts  

- Total:

`O(n log n)`  

- Worst case (sorted input):

`O(n²)`  

---


#### 🔹 populateSorted(int[] nums)


It inserts:

- Middle element first  
- Then recursively left and right  

- But it still calls insert n times.  

- Each insert = O(log n)  

- Total:

`O(n log n)`  

- However ⚠ Important:

- If instead of calling insert, we directly build tree using pointers:

Then it becomes:

`O(n)`  

- Much faster.

---

### Final Summary

| Topic        | Key Idea |
|-------------|----------|
| insert()    | Goes down one side only → O(log n) |
| balanced()  | Checks height difference + subtree balance |
| mid formula | Use start + (end-start)/2 |
| populate()  | O(n log n) |
| Traversals  | Inorder gives sorted output in BST |
| Stack       | Recursion builds downward, updates heights upward |

---

