# Stacks and Queues:-
![e](/images/stacks&queues1.png)
![e](/images/stacks&queues2.png)

---

```java
import java.util.*;

public class InbuiltExamplesOfStacksQueues {
    public static void main(String[] args){

        /*
         Use-cases of Stack, Queue & Deque:

         1) Stack:
            - Store "answer so far" in problems like:
              → undo/redo operations
              → expression evaluation (infix → postfix)
              → converting recursion to iteration (function calls stored in stack)
              → DFS traversal in graphs / trees
            - Binary Tree:
              → Inorder / Preorder / Postorder traversal (iterative using stack)

         2) Queue:
            - Used when order matters (first come, first served)
            - Binary Tree:
              → Level Order Traversal (BFS)
            - Real world:
              → CPU scheduling
              → Printer queue

         3) Deque:
            - When insertion/removal is needed from BOTH ends
            - Sliding Window problems
            - Can behave as:
              → Stack (push/pop from one end)
              → Queue (insert from rear, remove from front)
        */

        // ---------------- STACK ----------------
        // Stack is a class (legacy) in Java
        // Internally it uses a dynamic array (Vector)
        // Principle: LIFO / FILO (Last In First Out)
        // Time Complexity: push & pop → O(1)

        // Stack is an Abstract Data Type (ADT):
        // We only know operations (push, pop, peek),
        // internal implementation is hidden.

        Stack<Integer> stack = new Stack<>();
        stack.push(32);
        stack.push(3);
        stack.push(7);

        System.out.println(stack.pop()); // removes & returns top element → 7
        System.out.println(stack.pop()); // → 3
        System.out.println(stack.pop()); // → 32
        // Calling pop() on empty stack throws EmptyStackException


        // ---------------- QUEUE ----------------
        // Queue is an interface
        // Implemented here using LinkedList
        // FIFO / LILO (First In First Out)
        // Time Complexity: insertion & removal → O(1)

        // LinkedList maintains head & tail references
        // Hence insertion at tail & removal at head is efficient

        Queue<Integer> queue = new LinkedList<>();
        queue.add(32);
        queue.add(6);
        queue.add(1);
        queue.add(7);

        System.out.println(queue.peek());
        // peek(): retrieves head element WITHOUT removing it
        // returns null if queue is empty

        System.out.println(queue.remove());
        // remove(): retrieves & removes head
        // throws exception if queue is empty


        // ---------------- DEQUE ----------------
        // Deque = Double Ended Queue
        // Allows insertion & removal from BOTH ends
        // Implemented here using ArrayDeque

        // Why ArrayDeque is faster than Stack & LinkedList?
        // - Stack is synchronized → slower
        // - LinkedList has node overhead (extra memory + pointers)
        // - ArrayDeque uses resizable array → better cache locality

        // Not thread-safe → multiple threads can corrupt data
        // Null elements NOT allowed (helps distinguish empty vs null)

        Deque<Integer> deque = new ArrayDeque<>();

        deque.add(3);
        // add(): inserts element
        // throws exception if capacity is restricted & full

        deque.offer(4);
        // offer(): inserts element
        // returns false instead of throwing exception if insertion fails

        deque.offer(2);

        System.out.println(deque.remove());
        // remove(): removes & returns first element
        // throws exception if deque is empty

        System.out.println(deque.poll());
        // poll(): removes & returns first element
        // returns null if deque is empty

        System.out.println(deque.element());
        // element(): retrieves first element WITHOUT removing
        // throws exception if deque is empty

        System.out.println(deque.remove());

        System.out.println(deque.peek());
        // peek(): retrieves first element WITHOUT removing
        // returns null if deque is empty


        // ---------------- addAll() EXPLANATION ----------------
        /*
         addAll() works by iterating over the given collection
         and adding each element one by one at the end.

         Example:
         Deque<Integer> d1 = new ArrayDeque<>();
         d1.add(1);
         d1.add(2);

         Deque<Integer> d2 = new ArrayDeque<>();
         d2.add(3);
         d2.add(4);

         d1.addAll(d2);
         Result → d1 = [1, 2, 3, 4]
        */


        // ---------------- ERROR EXPLANATION ----------------
        // Deque.addFirst(3);  ❌ ERROR
        /*
         ERROR:
         "addFirst() cannot be referenced from a static context"

         Reason:
         - addFirst() is an instance method
         - You are calling it using class name (Deque)
         - Deque is an interface, not an object

         FIX:
         Call method using object reference
        */

        deque.addFirst(3); // ✅ Correct


        // ---------------- EQUIVALENT METHODS ----------------
        /*
         Queue method      ↔  Deque equivalent
         ------------------------------------
         add(e)            ↔  addLast(e)
         offer(e)          ↔  offerLast(e)
         remove()          ↔  removeFirst()
         poll()            ↔  pollFirst()
         element()         ↔  getFirst()
         peek()            ↔  peekFirst()
        */
    }
}
o/p:-
7
3
32
32
32
3
4
2
2
null
```
## Implementation of CustomStack class:-
CustomStack.java
```java
public class CustomStack {

    /*
     This is a FIXED SIZE stack (NOT resizable).
     If stack becomes full and we try to insert,
     an error message is shown or exception is thrown.
    */

    protected int[] data;
    private static final int DEFAULT_SIZE = 10;

    // ptr always points to the TOP element of stack
    // ptr = -1 → stack is empty
    int ptr = -1;

    // ---------------- CONSTRUCTORS ----------------

    public CustomStack() {
        /*
         this(DEFAULT_SIZE):

         - Calls the parameterized constructor of SAME class
         - Avoids code duplication
         - Equivalent to:
           new CustomStack(10)

         Execution flow:
         CustomStack() → CustomStack(int size) → array created
        */
        this(DEFAULT_SIZE);
    }

    public CustomStack(int size) {
        this.data = new int[size];
    }

    // ---------------- PUSH ----------------
    // Inserts element at top of stack
    public boolean push(int item) {
        if (isFull()) {
            System.out.println("Stack is Full");
            return false;
        }
        ptr++;
        data[ptr] = item;
        return true;
    }

    // ---------------- POP ----------------
    // Removes & returns last inserted element
    public int pop() throws Exception {
        if (isEmpty()) {
            throw new StackException("Cannot pop from an empty Stack!!");
        }

        int removed = data[ptr];
        ptr--;
        return removed;

        // Short version:
        // return data[ptr--];
    }

    // ---------------- PEEK ----------------
    // Returns top element WITHOUT removing it
    public int peek() throws Exception {
        if (isEmpty()) {
            throw new StackException("Cannot peek from an empty Stack!!");
        }
        return data[ptr];
    }

    // ---------------- HELPERS ----------------
    public boolean isFull() {
        // ptr == last valid index → stack is full
        return ptr == data.length - 1;
    }

    public boolean isEmpty() {
        return ptr == -1;
    }
}
```

DynamicStack.java
```java
public class DynamicStack extends CustomStack {

    // ---------------- CONSTRUCTORS ----------------

    public DynamicStack(int size) {
        // Calls parent (CustomStack) constructor
        // Initializes stack with given initial capacity
        super(size);
    }

    public DynamicStack() {
        // Calls default constructor of CustomStack
        // Uses DEFAULT_SIZE defined in CustomStack
        super();
    }

    /*
     Amortized Time Complexity of push():

     - Same behavior as ArrayList.add()
     - Most push() operations take O(1)
     - Occasionally, when array is full:
         → resizing takes O(n)
     - But resizing happens rarely
     - Hence amortized T.C. = O(1)
    */

    @Override
    public boolean push(int item) {

        /*
         This condition handles dynamic resizing:
         - When internal array becomes full
         - Create a new array of DOUBLE size
         - Copy existing elements into new array
        */
        if (this.isFull()) {

            // Create a new array with double capacity
            int[] temp = new int[2 * data.length];

            // Copy old stack elements into new array
            for (int i = 0; i < data.length; i++) {
                temp[i] = data[i];
            }

            // Update reference to point to new array
            data = temp;
        }

        /*
         At this point:
         - Stack is guaranteed NOT to be full
         - We can safely insert element using parent logic
        */
        return super.push(item);
    }
}
```

StackException.java
```java
// Custom checked exception for Stack-related errors
public class StackException extends Exception {

    /*
     Constructor of StackException

     How it works:
     - Accepts a custom error message
     - Passes that message to the parent Exception class
     - Parent class stores the message internally
    */
    public StackException(String message) {

        /*
         super(message):

         - Calls constructor of Exception class
         - Sets the exception message
         - This message can later be retrieved using getMessage()
        */
        super(message);
    }
}
```

Main.java
```java
public class Main {
    //method that creates and method that uses exception should use throws Exception keywords in their method signature.
    public static void main(String[] args) throws Exception {
           CustomStack stack = new CustomStack(5);

           stack.push(3);
           stack.push(4);
           stack.push(3);
           stack.push(3);
           stack.push(3);

           System.out.println(stack.pop());
           System.out.println(stack.pop());
           System.out.println(stack.pop());
           System.out.println(stack.pop());
           System.out.println(stack.pop());
          // System.out.println(stack.pop());//it will throw an exception as Cannot pop from an empty stack!!

           System.out.println();

           DynamicStack dynamicStack = new DynamicStack(2);
           dynamicStack.push(4);
           dynamicStack.push(4);
           dynamicStack.push(5);//No error even though size was initialized as 2.

           System.out.println(dynamicStack.pop());
           System.out.println(dynamicStack.pop());
           System.out.println(dynamicStack.pop());

           CustomStack customAccessDynamicVersionImplementation = new DynamicStack(4);





    }
}
o/p:-
3
3
3
4
3

5
4
4
```

## Implementation of CustomQueue:-
CustomQueue.java
```java
public class CustomQueue {

    /*
     Fixed-size array implementation of Queue (FIFO)

     NOTE:
     - This is NOT a circular queue
     - Removal is costly because elements are shifted
    */

    private int[] data;
    private static final int DEFAULT_SIZE = 10;

    /*
     'end' points to the NEXT free position in array

     Example:
     end = 0 → queue is empty
     insert(10) → data[0] = 10, end becomes 1
     insert(20) → data[1] = 20, end becomes 2
    */
    int end = 0;

    // ---------------- CONSTRUCTORS ----------------

    public CustomQueue() {
        // Calls parameterized constructor with default size
        this(DEFAULT_SIZE);
    }

    public CustomQueue(int size) {
        // Initializes queue with given capacity
        this.data = new int[size];
    }

    // ---------------- STATE CHECKS ----------------

    public boolean isFull() {
        /*
         Queue is full when:
         end == data.length
         (No more free space in array)
        */
        return end == data.length;
    }

    public boolean isEmpty() {
        /*
         Queue is empty when:
         end == 0
         (No elements inserted)
        */
        return end == 0;
    }

    // ---------------- INSERT ----------------
    /*
     Insertion Time Complexity: O(1)

     - Insert element at index 'end'
     - Increment end to point to next free slot
    */
    public boolean insert(int item) {
        if (isFull()) {
            return false;
        }
        data[end++] = item;
        return true;
    }

    // ---------------- REMOVE ----------------
    /*
     Removal Time Complexity: O(n)

     Reason:
     - First element (index 0) must be removed
     - Remaining elements are shifted one position left
    */
    public int remove() throws Exception {
        if (isEmpty()) {
            throw new Exception("Queue is Empty!!");
        }

        int removed = data[0];

        /*
         Shift all elements to the left by one index:
         data[1] → data[0]
         data[2] → data[1]
         ...
        */
        for (int i = 1; i < end; i++) {
            data[i - 1] = data[i];
        }

        end--; // Reduce queue size
        return removed;
    }

    // ---------------- FRONT ----------------
    /*
     Retrieves first element WITHOUT removing it
     Time Complexity: O(1)
    */
    public int front() throws Exception {
        if (isEmpty()) {
            throw new Exception("Queue is Empty!!");
        }
        return data[0];
    }

    // ---------------- DISPLAY ----------------
    /*
     Displays elements from front to rear
    */
    public void display() {
        for (int i = 0; i < end; i++) {
            System.out.print(data[i] + " ");
        }
        System.out.print("END");
    }
}
```

Main.java
```java
public class Main {
    //method that creates and method that uses exception should use throws Exception keywords in their method signature.
    public static void main(String[] args) throws Exception {
        CustomQueue customQueue = new CustomQueue(4);

        customQueue.insert(4);
        customQueue.insert(5);
        customQueue.insert(6);
        customQueue.insert(9);

        customQueue.display();

        System.out.println();
        System.out.println("Removed item:- " + customQueue.remove());

        customQueue.display();

    }
}
o/p:-
4 5 6 9 END
Removed item:- 4
5 6 9 END
```

## Implementation of CircularQueue class:-
CircularQueue.java
```java
public class CircularQueue {

    /*
     Circular Queue (Array-based)

     Key idea:
     - Uses modulo arithmetic to reuse array space
     - Avoids shifting elements
     - Insert and Remove both run in O(1)
    */

    /*
     'front' always points to the FIRST (oldest) element
     - Incremented when an element is removed
    */
    public int front = 0;

    /*
     'end' points to the NEXT free index for insertion
     - Insert element first, then increment end
     - Wrapped using modulo when it reaches array length
    */
    public int end = 0;

    public int[] data;
    private static final int DEFAULT_SIZE = 10;

    /*
     'size' tracks CURRENT number of elements in queue
     - Used to detect full and empty states
    */
    private int size = 0;

    // ---------------- CONSTRUCTORS ----------------

    public CircularQueue() {
        // Initializes queue with default capacity
        this(DEFAULT_SIZE);
    }

    public CircularQueue(int size) {
        // Initializes queue with user-defined capacity
        this.data = new int[size];
    }

    // ---------------- STATE CHECKS ----------------

    public boolean isFull() {
        /*
         Queue is full when:
         number of elements == array capacity

         We do NOT rely on 'end' because it keeps rotating
        */
        return size == data.length;
    }

    public boolean isEmpty() {
        // Queue is empty when it has zero elements
        return size == 0;
    }

    // ---------------- INSERT ----------------
    /*
     Time Complexity: O(1)

     Steps:
     1) Insert element at index 'end'
     2) Move 'end' circularly using modulo
     3) Increment current size
    */
    public boolean insert(int item) {
        if (isFull()) {
            return false;
        }

        data[end++] = item;
        end = end % data.length;
        size++;   // successful insertion increases element count

        return true;
    }

    // ---------------- REMOVE ----------------
    /*
     Time Complexity: O(1)

     Steps:
     1) Remove element from index 'front'
     2) Move 'front' circularly using modulo
     3) Decrement current size
    */
    public int remove() throws Exception {
        if (isEmpty()) {
            throw new Exception("Queue is Empty");
        }

        int removed = data[front];

        front++;
        front = front % data.length;
        size--;   // successful removal decreases element count

        return removed;
    }

    // ---------------- FRONT ----------------
    /*
     Retrieves the first element WITHOUT removing it
     Time Complexity: O(1)
    */
    public int front() throws Exception {
        if (isEmpty()) {
            throw new Exception("Queue is Empty!!");
        }
        return data[front];
    }

    // ---------------- DISPLAY ----------------
    /*
     Displays queue elements from front to rear
     - Traverses exactly 'size' elements
     - Correctly handles wrap-around
    */
    public void display() {
        int count = 0;
        int i = front;

        while (count < size) {
            System.out.print(data[i] + " -> ");
            i = (i + 1) % data.length;
            count++;
        }
        System.out.print("END");
    }
}
```

Main.java
```java
public class Main {
    //method that creates and method that uses exception should use throws Exception keywords in their method signature.
    public static void main(String[] args) throws Exception {
        CircularQueue customQueue = new CircularQueue(4);

        customQueue.insert(4);
        customQueue.insert(5);
        customQueue.insert(6);
        customQueue.insert(9);

        customQueue.display();

        System.out.println();

        System.out.println("Removed item:- " + customQueue.remove());

        customQueue.display();

    }
}
o/p:-
4 -> 5 -> 6 -> 9 -> END
Removed item:- 4
5 -> 6 -> 9 -> END
```
## Implementation of DynamicQueue class:-

```java
public class DynamicQueue extends CircularQueue{

    public DynamicQueue(int size){
        super(size);
    }

    public DynamicQueue(){
        super();
    }

    @Override
    public boolean insert(int item){
        //This(if condition)takes care of it(array) being full.(i.e.when array is full->double it's size.)
        if(this.isFull()){
            //double the ArraySize
            int[] temp = new int[2 * data.length];

            //Copy all previous items in data array
            for(int i = 0; i < data.length; i++){
                temp[i] = data[(front + i) % data.length];
            }
            //After copying elements from data to temp, update front and end.
            front = 0;
            end = data.length;
            data = temp;
        }

        //at this point we know that an array is not full
        //insert an item normally then...
        return super.insert(item);
    }
}
```


