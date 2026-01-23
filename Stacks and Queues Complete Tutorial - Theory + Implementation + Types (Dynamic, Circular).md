# Stacks and Queues:-
![e](/images/stack&q.png)

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
```
