# 1. LinkedList Lecture 1:-all images
![t](images/LinkedList_11.png)
![o](images/LinkedList_12.png)
![i](images/LinkedList_13.png)
# Singly Linked List – 
2. Limitations of Array / ArrayList:-
- Arrays
- Fixed size
- Cannot insert beyond capacity
- Requires continuous memory
- ArrayList
- When full, creates a new bigger array
- Copies all elements → costly

3. What is a Linked List?
- Non-contiguous memory allocation
- Nodes stored at random memory locations
- Connected using references
- Logical view:
- 3 → 4 → 1 → 8 → 9 → null
- 4. Node Structure
- Each node contains:
- Value
- Next reference
```java
private class Node {
    int value;      // data stored in node
    Node next;      // reference to next node

    Node(int value) {
        this.value = value;
        this.next = null; // default
    }

    Node(int value, Node next) {
        this.value = value;
        this.next = next; // tells which node comes next
    }
}
```
5. Singly Linked List
- Each node knows only the next node
- One-directional traversal

6. Head & Tail
- Head → first node
- Tail → last node
##### Data Members(head and tail)
- Store the reference of the first node in head.
- Store the reference of the last node in tail.
- Maintain the total number of nodes using size.
```java
private Node head;
private Node tail;
private int size;
```
7. Insert at First (O(1))
- Create a new node with the given value.
- Assign the current head reference to the new node’s next.
- Move head to point to the new node.
- If the list was empty, assign tail to head.
- Increment size.
```java
public void insertFirst(int value) {
    Node node = new Node(value);
    node.next = head;
    head = node;

    if (tail == null) {
        tail = head;
    }
    size++;
}
```
8. Insert at Last (O(1) using tail)
- Check whether the list is empty.
- If empty, perform insertion at first and stop.
- Create a new node with the given value.
- Assign the current tail’s next reference to the new node.
- Move tail to point to the new node.
- Increment size.
```java
public void insertLast(int value) {
    if (tail == null) {
        insertFirst(value);
        return;
    }
    Node node = new Node(value);
    tail.next = node;
    tail = node;
    size++;
}
```
9. Insert at Index (O(n))
- Check whether index is zero.
- If zero, perform insertion at first and stop.
- Check whether index equals size.
- If yes, perform insertion at last and stop.
- Start traversal from head.
- Move forward until reaching the node just before the given index.
- Create a new node and assign its next to the current node’s next.
- Update the current node’s next to the new node.
- Increment size.
```java
public void insert(int value, int index) {
    if (index == 0) {
        insertFirst(value);
        return;
    }
    if (index == size) {
        insertLast(value);
        return;
    }

    Node temp = head;
    for (int i = 1; i < index; i++) {
        temp = temp.next;
    }

    Node node = new Node(value, temp.next);
    temp.next = node;
    size++;
}
```
10. Display Linked List:-
- Create a temporary reference and assign it to head.
- Print the value of the current node.
- Move the temporary reference to the next node.
- Repeat until the temporary reference becomes null.
- Print END.
⚠️ Never move head during transversal.
```java
public void display() {
    Node temp = head;
    while (temp != null) {
        System.out.print(temp.value + " -> ");
        temp = temp.next;
    }
    System.out.println("END");
}
```
11. Delete First (O(1))
- Store the value of the head node.
- Move head to the next node.
- Check whether head becomes null.
- If yes, assign tail to null.
- Decrement size.
- Return the stored value.
```java
public int deleteFirst() {
    int value = head.value;
    head = head.next;

    if (head == null) {
        tail = null;
    }
    size--;
    return value;
}
```
12. Delete Last (O(n))
- Check whether the list contains only one node.
- If yes, perform delete-first and stop.
- Start traversal from head.
- Move forward until reaching the second-last node.
- Store the value of the tail node.
- Move tail to the second-last node.
- Assign tail’s next to null.
- Decrement size.
- Return the stored value.
```java
public int deleteLast() {
    if (size <= 1) {
        return deleteFirst();
    }

    Node secondLast = head;
    while (secondLast.next != tail) {
        secondLast = secondLast.next;
    }

    int value = tail.value;
    tail = secondLast;
    tail.next = null;
    size--;
    return value;
}
```
13. Delete at Index (O(n))
- Check whether index is zero.
- If zero, perform delete-first and stop.
- Check whether index is the last position.
- If yes, perform delete-last and stop.
- Start traversal from head.
- Move forward until reaching the node just before the index.
- Store the value of the node to be deleted.
- Update the next reference to skip the target node.
- Decrement size.
- Return the stored value.
```java
public int delete(int index) {
    if (index == 0) {
        return deleteFirst();
    }
    if (index == size - 1) {
        return deleteLast();
    }

    Node prev = head;
    for (int i = 1; i < index; i++) {
        prev = prev.next;
    }

    int value = prev.next.value;
    prev.next = prev.next.next;
    size--;
    return value;
}
```
14. Get Node at Index
- Start traversal from head.
- Move forward index number of times.
- Return the node reference at that position.
```java
public Node get(int index) {
    Node temp = head;
    for (int i = 0; i < index; i++) {
        temp = temp.next;
    }
    return temp;
}
```
15. Find a Value
- Start traversal from head.
- Compare the current node’s value with the target value.
- Return the node reference if a match is found.
- Move to the next node.
- Repeat until traversal ends.
- Return null if the value is not found.
```java
public Node find(int value) {
    Node node = head;
    while (node != null) {
        if (node.value == value) {
            return node;
        }
        node = node.next;
    }
    return null;
}
```
16. Time Complexity Summary
- Operation Time:-
- Insert First
O(1)
- Insert Last
O(1)
- Insert at Index
O(n)
- Delete First
O(1)
- Delete Last
O(n)
- Search
O(n)
- Display
O(n)

## Key Concept: Traversal vs Modification
- During traversal, the original linked list is NOT changed
- We only reassign a temporary reference variable
- Example:
node = node.next → moves the reference
- Does NOT modify the actual list
- Actual modification happens only with:
- node.next = something

👉 Traversal = reassignment, not modification

## Singly vs Doubly Linked List (Intuition)
- Singly Linked List = one‑sided love 😄
- Node knows next
- Cannot go backward

## Doubly Linked List = two‑way connection
- Node knows next AND previous
- DOUBLY LINKED LIST
- Why Doubly Linked List?
- In singly LL, no direct way to move backward
- Doubly LL adds one extra reference → previous
- Internal Structure of Doubly Linked List
- Every node contains:

value,

next,

previous

- Rules:
head.previous = null &

tail.next = null

### Node Structure (Doubly Linked List)
```java
private class Node {
    int value;
    Node next;
    Node previous;


    Node(int value) {
        this.value = value;
    }


    Node(int value, Node next, Node previous) {
        this.value = value;
        this.next = next;
        this.previous = previous;
    }
}
```
##### Insert First in Doubly Linked List Logic :
- Create new node
- node.next = head
- node.previous = null
- If head != null → head.previous = node
- head = node

⚠️ Null check is mandatory to avoid NullPointerException
```java
public void insertFirst(int value) {
    Node node = new Node(value);
    node.next = head;
    node.previous = null;


    if (head != null) {
        head.previous = node;
    }
    head = node;
}
```
⏱ Time Complexity: O(1)

##### Display Doubly Linked List (Forward)
Important Rule:
- Use temporary variable, never move head
```java
public void display() {
    Node node = head;
    while (node != null) {
        System.out.print(node.value + " -> ");
        node = node.next;
    }
    System.out.println();
}
```
##### Display Doubly Linked List (Reverse) Logic:
- First traverse forward to reach last node
- Then move backward using previous
```java
public void displayReverse() {
    Node node = head;
    Node last = null;


    while (node != null) {
        last = node;
        node = node.next;
    }


    while (last != null) {
        System.out.print(last.value + " -> ");
        last = last.previous;
    }
    System.out.println();
}
```
##### Insert Last in Doubly Linked List (No Tail) Logic:
- Create new node
- If head == null:
- head = node
- node.previous = null
- return
- Traverse till last (last.next == null)
- last.next = node
- node.previous = last
- node.next = null
```java
public void insertLast(int value) {
    Node node = new Node(value);
    node.next = null;


    if (head == null) {
        node.previous = null;
        head = node;
        return;
    }


    Node last = head;
    while (last.next != null) {
        last = last.next;
    }


    last.next = node;
    node.previous = last;
}
```
⏱ Time Complexity: O(n)

##### Insert After a Given Value (Doubly Linked List)
Problem:
- Insert newValue after a node containing value:-
- Find node p
- Create new node
- node.next = p.next
- p.next = node
- node.previous = p
- If node.next != null → node.next.previous = node
⚠️ Null check required when inserting after last node
```java
public void insertAfter(int value, int newValue) {
    Node p = find(value);
    if (p == null) return;


    Node node = new Node(newValue);
    node.next = p.next;
    p.next = node;
    node.previous = p;


    if (node.next != null) {
        node.next.previous = node;
    }
}
```
⏱ Time Complexity: O(n)

# CIRCULAR LINKED LIST
Key Property
- No node points to null
- Last node points back to head
```java
Node Structure (Circular LL)
private class Node {
    int value;
    Node next;


    Node(int value) {
        this.value = value;
    }
}
```
Circular Linked List Fields
```java
private Node head;
private Node tail;
```
##### Insert in Circular Linked List Logic:
- Create new node
- If list is empty:
- head = node
- tail = node
- node.next = head
- Else:
- tail.next = node
- node.next = head
- tail = node
```java
public void insert(int value) {
    Node node = new Node(value);


    if (head == null) {
        head = node;
        tail = node;
        node.next = head;
        return;
    }


    tail.next = node;
    node.next = head;
    tail = node;
}
```
##### Display Circular Linked List Rule:
- Must print at least once → use do‑while
```java
public void display() {
    if (head == null) return;


    Node node = head;
    do {
        System.out.print(node.value + " -> ");
        node = node.next;
    } while (node != head);
    System.out.println();
}
```
⏱ Time Complexity: O(n)

##### Delete Value in Circular Linked List
- Case 1: Empty List
- Return

- Case 2: Delete Head
- head = head.next
- tail.next = head

- Case 3: Delete Other Node
- Traverse
- Check node.next.value
- Skip node
```java
public void delete(int value) {
    if (head == null) return;


    Node node = head;


    if (node.value == value) {
        head = head.next;
        tail.next = head;
        return;
    }


    do {
        Node n = node.next;
        if (n.value == value) {
            node.next = n.next;
            break;
        }
        node = node.next;
    } while (node != head);
}
```
⏱ Time Complexity: O(n)

---
# My Codes + Notes:-(Even if you read my notes + kuanl kushwaha class notes(white board notes) = enough)(else you can read elaborated explanation(chatgpt notes) if you are not understanding my notes)
#### Singly LinkedList Implementation from Scratch:-first apply dot operator on node like node.next etc and then on next and prev nodes.
![p](images/SLL_1.jpg)
![r](images/SLL_2.jpg)
![u](images/SLL_3.jpg)
```java
package LinkedList;

public class SinglyLinkedList {

    // Reference to the first node of the linked list
    private Node head;

    // Reference to the last node of the linked list
    private Node tail;

    // Stores the total number of nodes in the linked list
    private int size;

    // Constructor to initialize an empty Singly linked list
    public SinglyLinkedList() {
        this.size = 0;
        // head and tail are null by default
    }
    //Inserting at first position before head in Singly Linked List
    public void insertFirst(int val){
        Node node = new Node(val);
        node.next = head;
        head = node;
        if(tail == null){
            tail = head;
        }
        size += 1;//to increase size of Linked List by 1
    }
    //Display LinkedList
    public void display(){
        Node temp;
        temp = head;
        while(temp != null){
            System.out.print(temp.value + " -> ");
            temp = temp.next;
        }
        System.out.print("END");
        System.out.println();
    }
    //Insert at Last position(using tail):-O(1)
    public void insertLast(int val){
        if(tail == null){
            this.insertFirst(val);
            return;//as if tail == null => tail.next = null.next => will give NullPointerException
            //You can't use dot operator for null.
                    }
        Node node = new Node(val);
        tail.next = node;
        tail = node;
        size += 1;
    }
    //Insert at particular index:-O(n)
    public void insert(int val, int index){
         if(index == 0){
             insertFirst(val);
             return;
         }
         if(index == size){
             insertLast(val);
             return;
         }
         //start checking from head
         Node temp = head;//head is at 0th index.therefore temp is already at head hence start temp. from 1st index inside for loop,at during first iteration we are assigning temp to 1st index hence i should be 1 at that time.
         //if index is 3 then go till 2nd index to set element at 3rd index by doing temp.next = node;
        for(int i = 1; i < index; i++){
             temp = temp.next;
        }
        Node node = new Node(val, temp.next);//current.next = temp.next as second parameter is taking ref var.pointing to next Node of temp Node.
        //now next Node of node will automatically set to temp.next using constructor now we only need to set previous node of node(i.e. of newNode)
        temp.next = node;
        size += 1;
    }
    //DeleteFirst :- O(1)
     public int deleteFirst(){
        int val = head.value;
        head = head.next;
        if(head == null){
            tail = null;
        }
        size -= 1;
        return val;
     }
    //DeleteLast :- O(1)
    public int deleteLast(){
        if(size <= 1){
            return deleteFirst();
        }
        int val = tail.value;
        Node secondLastNode = get(size - 2);//to get Node which is just before tail Node
        tail = secondLastNode;
        tail.next = null;//ref var. pointing to previous last item(that arrow) and last item will be removed by Garbage collector.
        size -= 1;
        return val;
    }
    //Delete a particular node :- O(1)
    public int Delete(int index){
        if(index == 0){
            return deleteFirst();
        }
        if(index == size - 1){
            return deleteLast();
        }
        Node prev = get(index - 1);
        int val = prev.next.value;
        prev.next = prev.next.next;
        size -= 1;
        return val;
    }
    //to get the node having particular value passed as parameter.
    public Node find(int val){
        Node node = head;
        while(node != null) {
            if (node.value == val) {
                return node;
            }
            node = node.next;
        }
        return null;
    }

    //to get/set ref.var pointing to the node which is at particular that index.
    public Node get(int index){
        Node node = head;
        for(int i = 1; i <= index; i++){
            node = node.next;
        }
        return node;
    }

    // Inner class representing a single node of the linked list
    private class Node {

        // Value stored in the current node
        private int value;

        // Reference variable pointing to the next node
        private Node next;

        // Constructor that initializes the node with a value
        // Since next is not provided, it points to null by default
        public Node(int value) {
            this.value = value;
            // next is automatically set to null
        }

        // Constructor that initializes both value and next reference
        public Node(int value, Node next) {
            this.value = value;
            this.next = next; // Explicitly assigning the next node(i.e.assigning ref. var to next Node)
        }
    }
}
```
Main.java
```java
package LinkedList;

public class Main {
    public static void main(String[] args){
        SinglyLinkedList list = new SinglyLinkedList();
        //Insert at first position->O(1)
        list.insertFirst(3);
        list.insertFirst(4);
        list.insertFirst(5);
        //display Singly LinkedList ->O(n)
        list.display();
        //Insert at last position
        list.insertLast(14);
        list.display();
        //Insert at particular position
        list.insert(90, 2);
        list.display();
        //delete first Node
        System.out.println(list.deleteFirst());
        list.display();
        //delete last Node
        System.out.println(list.deleteLast());
        list.display();
        System.out.println(list.Delete(2));
        list.display();
        //display Node having value 90.
        System.out.println(list.find(90));

    }
}
o/p:-
5 -> 4 -> 3 -> END
5 -> 4 -> 3 -> 14 -> END
5 -> 4 -> 90 -> 3 -> 14 -> END
5
4 -> 90 -> 3 -> 14 -> END
14
4 -> 90 -> 3 -> END
3
4 -> 90 -> END
LinkedList.SinglyLinkedList$Node@34a245ab
```
---
#### Doubly LinkedList Implementation from Scratch-
![w](images/DLL_1.jpg)
```java
package LinkedList;

public class DoublyLinkedList {
    private Node head;
    private Node tail;
    private int size;

    public DoublyLinkedList(){
        this.size = 0;
    }

    public void insertFirst(int value){
        Node node = new Node(value);
        node.next = head;
        node.prev = null;
        if(head != null){
            head.prev = node;
        }
        head = node;
        if(tail == null){
            tail = head;
        }
        size++;
    }
    //InsertLast :- O(1)
    // Insert at Last : O(n)
    public void insertLast(int value) {
        Node node = new Node(value);

        // If list is empty
        if (head == null) {
            node.prev = null;
            node.next = null;
            head = node;
            size++;
            return;
        }

        // Traverse to find last node
        Node last = head;
        while (last.next != null) {
            last = last.next;
        }

        // Link new node at the end
        last.next = node;
        node.prev = last;
        node.next = null;

        size++;
    }
    //Insert after a particular node if value of that node is given:- O(n)
    public void insert(int after, int value){
        Node p = find(after);
        if(p == null){
            System.out.println("Node having value " + after + " doesn't exist");
            return;
        }
        Node node = new Node(value);
        node.next = p.next;
        node.prev = p;
        //if you are using dot operator on existing ref. var other than node then check for NullPointerException
        if(p.next != null){
            p.next.prev = node;
        }
        else{
            insertLast(value);
        }
        p.next = node;
        size++;
    }

    //to display DLL
    public void display(){
        Node node = head;
        Node last = null;
        while(node != null){
            System.out.print(node.value + " -> ");
            node = node.next;
        }
        System.out.print("END");
        System.out.println();
    }
    //to display DLL in Reverse order(using tail)
    public void displayRev(){
        Node node = tail;
        while(node != null){
            System.out.print(node.value + " -> ");
            node = node.prev;
        }
        System.out.print("START");
        System.out.println();
    }
    //to display DLL in Reverse order(using last ref var./Node)
    public void displayRevUsinglast(){
        //used first while loop to find tail = last Node/ref var. pointing to last Node
        Node node = head;
        Node last = null;
        while(node != null){
            last = node;
            node = node.next;
        }
        //to print DLL using last ref var.
        while(last != null){
            System.out.print(last.value + " -> ");
            last = last.prev;
        }
        System.out.print("START");
        System.out.println();
    }
    //to get the node having particular value passed as parameter.
    public Node find(int val){
        Node node = head;
        while(node != null) {
            if (node.value == val) {
                return node;
            }
            node = node.next;
        }
        return null;
    }




      private class Node{
          int value;
          Node next;
          Node prev;

          public Node(int value){
              this.value = value;
          }

          public Node(int value, Node next, Node prev){
              this.value = value;
              this.next = next;
              this.prev = prev;
          }
      }


}
```
Main.java
```java
package LinkedList;

public class Main {
    public static void main(String[] args){
        DoublyLinkedList list = new DoublyLinkedList();
        //Insert at first position->O(1)
        list.insertFirst(3);
        list.insertFirst(4);
        list.insertFirst(5);
        //display Doubly LinkedList ->O(n)
        list.display();
        //display Doubly LinkedList in Reverse Order using tail->O(n)
        list.displayRev();
        //display Doubly LinkedList in Reverse Order without using tail->O(n)
        list.displayRevUsinglast();
        //InsertLast:-O(1)
        list.insertLast(14);
        list.display();
        //Insert after a certain node having value given as first parameter(after) in insert()
        list.insert(4, 15);
        list.display();


    }
}
o/p:-
5 -> 4 -> 3 -> END
3 -> 4 -> 5 -> START
3 -> 4 -> 5 -> START
5 -> 4 -> 3 -> 14 -> END
5 -> 4 -> 15 -> 3 -> 14 -> END
```
#### Circular LinkedList Implementation from Scratch:-
![y](images/CLL_1.jpg)
```java
package LinkedList;

public class CircularLinkedList {
    private Node head;
    private Node tail;
    private int size;

    public CircularLinkedList(){
        this.head = null;
        this.tail = null;
        this.size = 0;
    }
    //InsertFirst/InsertLast:- O(1)
    public void insert(int value){
        Node node = new Node(value);
        if(head == null){
            head = node;
            tail = node;
            return;
        }
        node.next = head;
        tail.next = node;
        tail = node;
        size++;
    }
    //Display CLL
    public void display(){
        Node node = head;
        if(head != null){
            do{
                System.out.print(node.value + " -> ");
                node = node.next;
            }while(node != head);
        }
        System.out.println("HEAD");
    }
    //Delete a particular value
    public void delete(int value){
        Node node = head;
        if(node == null){
            return;
        }
        if(node.value == value){
            head.next = head;
            tail.next = head;
            return;
        }
        do{
            Node n = node.next;
            if(n.value == value){
                node.next = n.next;
                return;
            }
            node = node.next;
        }while(node != head);
        //otherwise
        System.out.println("Value that you want to delete Doesn't exist");

    }
    
      private class Node{
          int value;
          Node next;


          public Node(int value){
              this.value = value;
          }

          public Node(int value, Node next){
              this.value = value;
              this.next = next;
          }
      }


}
```
Main.java
```java
package LinkedList;

public class Main {
    public static void main(String[] args){
        CircularLinkedList list = new CircularLinkedList();
        //Insert at first position->O(1)
        list.insert(3);
        list.insert(4);
        list.insert(5);
        //display Doubly LinkedList ->O(n)
        list.display();
        //delete 4
        list.delete(4);
        list.display();



    }
}
o/p:-
3 -> 4 -> 5 -> HEAD
3 -> 5 -> HEAD
```
---
