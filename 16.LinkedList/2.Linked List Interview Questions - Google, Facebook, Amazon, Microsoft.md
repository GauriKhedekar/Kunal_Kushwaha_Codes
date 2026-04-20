# Linked-List Questions:-
![u](images/LLQ.png)
![o](images/LLQ2.png)
![r](images/LLQ3.png)
![p](images/LLQ4.png)
![r](images/LLQ5.png)
##### Steps to solve any Linked List Problem:-
- 1)take any 1 example i/p
- 2)see how our output would look like or wat we are trying to achieve
- 3)see which all nodes and branches are required to achieve final output and code according to it.
- ---
#### Q-01: Recursive Insertion in LinkedList:-for more understnading/figure watch/read his class notes....
```java
// Insert a node at a given index using recursion
// This method is called by the user
public void insertRec(int val, int index) {
    // Start recursion from the head node
    // The returned node becomes the new head (important!)
    head = insertRec(val, index, head);
}

// Recursive helper function
private Node insertRec(int val, int index, Node node) {

    // BASE CASE:
    // When index becomes 0, we have reached the position
    // where the new node should be inserted
    if(index == 0){
        // Create a new node with value 'val'
        // and point it to the current node
        Node temp = new Node(val, node);

        // Increase the size of the linked list
        size++;

        // Return the newly created node
        // This node will be linked by the previous recursive call
        return temp;
    }

    // RECURSIVE CALL:
    // Move to the next node
    // Reduce index by 1 as we move one position forward
    node.next = insertRec(val, index - 1, node.next);

    // Return the current node so the links remain intact
    return node;
}

```
#### Q2) Remove Duplicates from sorted list:-
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode node = head;

        while (node != null && node.next != null) {
            if (node.val == node.next.val) {
                // Remove duplicate
                node.next = node.next.next;
            } else {
                // Move forward only when values are different
                node = node.next;
            }
        }

        return head;
    }
}
Input: head = [1,1,2]
Output: [1,2]
```
#### Q3)Merge 2 sorted lists:- 
- You are given the heads of two sorted linked lists list1 and list2.
- Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.
- Return the head of the merged linked list.
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummyNode = new ListNode(-1);/*we are gonna return dummyNode.next henc initialize it's value to any number as we are not gonna use it anywhere in the code*/
        ListNode temp = dummyNode;/*we have used dummyNode to act it as head so that even if we move temp node we can return head i.e dummyNode in the last(i.e.dummyNode.next) just like we return head when head is given*/
        while(list1 != null && list2 != null){
            if(list1.val <= list2.val){
                temp.next = list1;
                list1 = list1.next;
            }
            else{
                temp.next = list2;
                list2 = list2.next;
            }
            temp = temp.next;
        }
        //add remaining nodes from any one of the lists
        while(list1 != null){
            temp.next = list1;
            temp = temp.next;
            list1 = list1.next;
        }
        while(list2 != null){
            temp.next = list2;
            temp = temp.next;
            list2 = list2.next;
        }        
    return dummyNode.next;

    }
}
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```
#### Q4)Linked List Cycle:-
- Given head, the head of a linked list, determine if the linked list has a cycle in it.
- There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.
- Return true if there is a cycle in the linked list. Otherwise, return false.
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;//This will move 2 steps ahead in each iteration
        ListNode slow = head;//This will move 1 step ahead in each iteration

        while(fast != null && fast.next != null){
             slow = slow.next;
             fast = fast.next.next;
             //when fast & slow pointer meet each other that means cycle is detected.
             if(fast == slow){
                return true;
             }

        }
        return false;

    }
}
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```
#### Q5)Find length of linked-List cycle:-
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public int len(ListNode head) {
        ListNode fast = head;//This will move 2 steps ahead in each iteration
        ListNode slow = head;//This will move 1 step ahead in each iteration

        while(fast != null && fast.next != null){
             slow = slow.next;
             fast = fast.next.next;
             //when fast & slow pointer meet each other that means cycle is detected.
             if(fast == slow){
               ListNode temp = slow;//increment the length, until temp reaches slow ListNode again... 
               int length = 0;
               do{
                 length++;
                 temp = temp.next;
             }while(temp != slow);
             return length;

        }
        return 0;

    }
}
```
#### Q6)Linked-List Cycle II:-
- Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.
- There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.
- Do not modify the linked list.
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head == null || head.next == null) return null;
        ListNode slow = head;
        ListNode fast = head;
        int length = 0;
        //run the frst while loop until fast pointer is thrown outside the Linked-List
        //step 1:-Find the length of Linked-List cycle
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(fast == slow){
                ListNode temp = slow;
                do{
                    length = length + 1;
                    temp = temp.next;
                }while(temp != slow);
                break;//important
            }
        }
        //if no cycle is detected return null
        if(length == 0) return null;
        ListNode f = head;
        ListNode s = head;
        //step 2:-move second pointer till length of cycle
        for(int i = 0; i < length; i++){
            s = s.next;
        }

        //step 3:-move both first and second pointers until they meet each other as both are k distance away from each other
        while(f != s){
            f = f.next;
            s = s.next;
        }
        return f;//or s

    }
}
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```
#### Q7)Happy Number
- Write an algorithm to determine if a number n is happy.
- A happy number is a number defined by the following process:
- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
- Those numbers for which this process ends in 1 are happy.
- Return true if n is a happy number, and false if not.
```java
class Solution {
    public boolean isHappy(int n) {
        int first = n;//move this pointer by 1,i.e. find square of digits of only one number.
        int second = n;//move this pointer by 2,i.e. find square of digits of first number and then square of digits of (square of first number)
        //if first becomes equal to second that means cycle is detected and that number's addition of digits of squares are never gonna be 1
        do{
            first = squareOfDigits(first);
            second = squareOfDigits(squareOfDigits(second));
        }while(first != second);
    //it will work for happy number as well ,if you want to know you can dry run by taking any example of happy number
    if(first == 1)//i.e sum of square of digits becomes 1
    {
         return true;
    }
    return false;
}

public static int squareOfDigits(int number){
    int ans = 0;
    while(number > 0){
        int lastDigit = number % 10;
        ans += (lastDigit * lastDigit);
        number /= 10;
    }
    return ans;
}
}
Example 1:

Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```
#### Q8)Middle of the LinkedList:-
- Given the head of a singly linked list, return the middle node of the linked list.
- If there are two middle nodes, return the second middle node.
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        //when fast pointer reaches at the end, slow pointer reaches at the middle of the Linked-List
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```
#### Q9)Sort List:-
- mergeSort :- T.C:-O(nlogn), S.C:-O(1)
- Given the head of a linked list, return the list after sorting it in ascending order.
- here,we are using recursion just like we used in merge sort and we are cutting list from head till node just before mid and from mid till tail in the getMid():-
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode mid = getMid(head);
        ListNode left = sortList(head);/*as we have broken the list hence if we sort the List from head it will sort from head till ListNode before mid*/
        ListNode right = sortList(mid);//and it will sort the ListNode from mid till tail.
        return merge(left, right);
    }
    //to get the middle node of the LInked-List
    public ListNode getMid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = null;
        //when fast pointer reaches at the end, slow pointer reaches at the middle of the Linked-List
        while(fast != null && fast.next != null){
            prev = slow;/*This pointer will be at poisition just before slow/mid, at the end of this while loop*/
            slow = slow.next;
            fast = fast.next.next;
        }
        //check for nullPointer exception as well for prev
        if (prev != null) {
        prev.next = null;  /*CUT the list from head to ListNode present before mid and midNode to tail*/
    }
        return slow;
    }
    //It merges two lists
    public ListNode merge(ListNode list1, ListNode list2) {
        ListNode dummyNode = new ListNode(-1);/*we are gonna return dummyNode.next henc initialize it's value to any number as we are not gonna use it anywhere in the code*/
        ListNode temp = dummyNode;/*we have used dummyNode to act it as head so that even if we move temp node we can return head i.e dummyNode in the last(i.e.dummyNode.next) just like we return head when head is given*/
        while(list1 != null && list2 != null){
            if(list1.val <= list2.val){
                temp.next = list1;
                list1 = list1.next;
            }
            else{
                temp.next = list2;
                list2 = list2.next;
            }
            temp = temp.next;
        }
        //add remaining nodes from any one of the lists
        while(list1 != null){
            temp.next = list1;
            temp = temp.next;
            list1 = list1.next;
        }
        while(list2 != null){
            temp.next = list2;
            temp = temp.next;
            list2 = list2.next;
        }        
    return dummyNode.next;

    }
}
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```
- bubbleSort:-
```java
// Public method to start Bubble Sort on the linked list
public void bubbleSort() {
    // We start with row = size - 1 because:
    // In bubble sort, after each pass, the largest element
    // gets placed at the end of the list.
    // So after (size - 1) passes, the list becomes sorted.
    bubbleSort(size - 1, 0);
}

// Recursive bubble sort method
// row -> number of comparisons left in current pass
// col -> current index being compared
private void bubbleSort(int row, int col) {

    // Base condition:
    // When row becomes 0, it means all passes are complete
    // and the list is fully sorted
    if (row == 0) {
        return;
    }

    // If col is less than row, we can compare col and col + 1
    // We stop at 'row' because the last 'row' elements
    // are already in their correct positions
    if (col < row) {

        // Get the current node (first) at index 'col'
        Node first = get(col);

        // Get the next node (second) at index 'col + 1'
        Node second = get(col + 1);

        // If values are in wrong order, we need to swap nodes
        if (first.value > second.value) {

            // CASE 1: first node is the head of the list
            // After swapping, 'second' becomes the new head
            if (first == head) {
                head = second;               // update head
                first.next = second.next;    // detach first
                second.next = first;         // place first after second
            }

            // CASE 2: second node is the tail of the list
            // After swapping, 'first' becomes the new tail
            else if (second == tail) {
                Node prev = get(col - 1);    // node before 'first'
                prev.next = second;          // connect prev to second
                second.next = first;         // swap nodes
                first.next = null;           // tail must point to null
                tail = first;                // update tail
            }

            // CASE 3: both nodes are in the middle of the list
            else {
                Node prev = get(col - 1);    // node before 'first'
                prev.next = second;          // connect prev to second
                first.next = second.next;    // detach first
                second.next = first;         // swap nodes
            }
        }

        // Move to the next comparison in the same pass
        bubbleSort(row, col + 1);
    }

    // If col has reached row, one full pass is complete
    // Reduce row and start the next pass from col = 0
    else {
        bubbleSort(row - 1, 0);
    }
}
```
#### Q10) Reverse LinkedList (Recursive):-
```java
public void reverse(){
       if(head == null || head.next == null) return;
        reverse(head);
    }

    //Reverse a Linked-List :- Recursive approach
    private void reverse(Node node){
        if(node == tail){
            head = node;
            return;
        }
        //Otherwise do node.next
        reverse(node.next);

        tail.next = node;
        tail = node;
        tail.next = null;
    }
```

####  Q11) Reverse LinkedList (Iterative):-
- Given the head of a singly linked list, reverse the list, and return the reversed list.
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
       if(head == null || head.next == null){
        return head;
       } 
       ListNode prev = null;
       ListNode present = head;
       ListNode next = head.next;

       while(present != null){
        present.next = prev;
        prev = present;
        present = next;
        if(next != null){
            next = next.next;
        }
       }
       head = prev;
       return head;
    }
}
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```
#### Q12) Reverse LinkedList II:-
- Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.
```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if(head == null || head.next == null) return head;
        // If left == right, nothing to reverse
        if (left == right) return head;

        // prev will finally point to the head of reversed sublist
        ListNode prev = null;
        ListNode present = head;

        // Step 1: Move present to the left-th node
        // prev will end at (left - 1)th node
        // Example: left = 2
        // After loop:
        // prev -> 1
        // present -> 2
        for (int i = 0; i < left - 1; i++) {
            prev = present;
            present = present.next;
        }

        // last points to node before reversal
        // newEnd points to first node of sublist (will become last after reversal)
        ListNode last = prev;       // Node 1
        ListNode newEnd = present;  // Node 2

        // next pointer for safe traversal
        ListNode next = present.next;

        // Step 2: Reverse nodes from left to right
        // Number of nodes = (right - left + 1)
        for (int i = 0; i < right - left + 1; i++) {
            present.next = prev;  // reverse link
            prev = present;       // move prev forward
            present = next;       // move present forward

            if (next != null) {
                next = next.next;
            }
        }

        /*
         At this point:
         prev -> head of reversed sublist (node 4)
         present -> node after right (node 5)
         newEnd -> tail of reversed sublist (node 2)
        */

        // Step 3: Connect first part with reversed sublist
        if (last != null) {
            // Case 1: Reversal does NOT start from head
            // Example: 1 -> 4
            last.next = prev;
        } else {
            // Case 2: Reversal starts from head
            // head must be updated
            head = prev;
        }

        // Step 4: Connect reversed sublist with remaining list
        // Example: 2 -> 5
        newEnd.next = present;

        return head;
    }
}
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```
#### Q13) Palindrome LinkedList:-
- Given the head of a singly linked list, return true if it is a palindrome or false otherwise.
![r](images/LL_reverse_logic.jpg)
- “If both B and D point to C, then how is this a singly linked list?”->A singly linked list means each node has only ONE outgoing pointer (next),
NOT that a node can have only one incoming pointer->Incoming pointers are unrestricted.:-
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode mid = middleNode(head);
        ListNode headSecond = reverseList(mid);//it will store head of reversed list i.e. original tail/Last ListNode
        ListNode reReverseHead = headSecond;//Re-reverse list from mid ListNode of reversed List to get original List

    while(head != null && headSecond != null){
        if(head.val != headSecond.val){
            break;//we haven't returened false from here as we have to re-Reverse the LinkedList to get original LinkedList
        }
        head = head.next;
        headSecond = headSecond.next;
    }  

    //Re-Reverse list in the end using reReverseHead pointer
    reverseList(reReverseHead);
    //if we have traversed the entire list without breaking in middle then any one of the ListNode from below must have become null
    if(headSecond == null || head == null){
        return true;
    }    
    return false;
    }
    //To find middle Node of a Linked-List
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        //when fast pointer reaches at the end, slow pointer reaches at the middle of the Linked-List
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    //To Reverse a Linked-List
    public ListNode reverseList(ListNode head) {
       if(head == null || head.next == null){
        return head;
       } 
       ListNode prev = null;
       ListNode present = head;
       ListNode next = head.next;

       while(present != null){
        present.next = prev;
        prev = present;
        present = next;
        if(next != null){
            next = next.next;
        }
       }
       head = prev;
       return head;
    }
}
Input: head = [1,2,2,1]
Output: true
```
#### Q14)Reorder LinkedList:-
- You are given the head of a singly linked-list. The list can be represented as:
- L0 → L1 → … → Ln - 1 → Ln
- Reorder the list to be on the following form:
- L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
- You may not modify the values in the list's nodes. Only nodes themselves may be changed.
![u](images/dryrun_reorder_list.jpg)
![r](images/dryrun_reorder_list2.jpg)
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public void reorderList(ListNode head) {
        if(head == null || head.next == null) return;

        ListNode mid = middleNode(head);

        ListNode hs = reverseList(mid);  
        ListNode hf = head;

        while(hf != null && hs != null){
            //temp node:- to store next nodes of hf and hs and upate them'(hf and hs) to next.
            ListNode temp = hf.next;
            hf.next = hs;
            hf = temp;

            temp = hs.next;
            hs.next = hf;
            hs = temp; 
        }
        //When we have reached at the end and hf.next is not pointing to null if hf != null then point it to null as hs has already becme null as we have come out of loop because of it.
        if(hf != null){
            hf.next = null;
        }

    }

        //To find middle Node of a Linked-List
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        //when fast pointer reaches at the end, slow pointer reaches at the middle of the Linked-List
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    //To Reverse a Linked-List
    public ListNode reverseList(ListNode head) {
       if(head == null || head.next == null){
        return head;
       } 
       ListNode prev = null;
       ListNode present = head;
       ListNode next = head.next;

       while(present != null){
        present.next = prev;
        prev = present;
        present = next;
        if(next != null){
            next = next.next;
        }
       }
       head = prev;
       return head;
    }
    
}
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```
#### Q15) Reverse k-Nodes in LinkedList:-
- Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.
- k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.
- You may not alter the values in the list's nodes, only nodes themselves may be changed.
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {

    public ListNode reverseKGroup(ListNode head, int k) {

        // Base case:
        // If list is empty or has only one node, no reversal needed
        if (head == null || head.next == null) return head;

        // prev: points to the node BEFORE the current k-group
        // present: points to the current node being processed
        ListNode prev = null;
        ListNode present = head;

        while (true) {

            // last: node just before the current group
            // newEnd: first node of current group
            // (after reversal, newEnd becomes the last node of the group)
            ListNode last = prev;
            ListNode newEnd = present;

            // Step 1: Check if k nodes exist starting from 'present'
            ListNode temp = present;
            int count = 0;
            while (temp != null && count < k) {
                temp = temp.next;
                count++;
            }

            // If fewer than k nodes remain, do not reverse
            if (count < k) {
                break;
            }

            // Step 2: Reverse exactly k nodes
            // next is used to safely move forward while reversing links
            ListNode next = present.next;
            prev = null;

            for (int i = 0; i < k; i++) {
                present.next = prev;   // reverse current link
                prev = present;        // move prev forward
                present = next;        // move present forward
                if (next != null) {
                    next = next.next;
                }
            }

            /*
             After reversal:
             prev     -> head of reversed k-group
             present  -> first node after the reversed group
             newEnd   -> tail of reversed group
            */

            // Step 3: Connect previous part of list to reversed group
            if (last != null) {
                // Reversal does NOT start from head
                last.next = prev;
            } else {
                // Reversal starts from head
                head = prev;
            }

            // Step 4: Connect reversed group with the remaining list
            newEnd.next = present;

            // If no nodes remain, stop processing
            if (present == null) {
                break;
            }

            // Prepare for next group
            prev = newEnd;
        }

        return head;
    }
}
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```
#### Q16)Reverse Alternate k-Nodes in LinkedList:-
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {

    public ListNode reverseKGroup(ListNode head, int k) {

        // Base case:
        // If list is empty or has only one node, no reversal needed
        if (head == null || head.next == null) return head;

        // prev: points to the node BEFORE the current k-group
        // present: points to the current node being processed
        ListNode prev = null;
        ListNode present = head;

        while (present != null) {

            // last: node just before the current group
            // newEnd: first node of current group
            // (after reversal, newEnd becomes the last node of the group)
            ListNode last = prev;
            ListNode newEnd = present;

            // Step 1: Check if k nodes exist starting from 'present'
            ListNode temp = present;
            int count = 0;
            while (temp != null && count < k) {
                temp = temp.next;
                count++;
            }

            // If fewer than k nodes remain, do not reverse
            if (count < k) {
                break;
            }

            // Step 2: Reverse exactly k nodes
            // next is used to safely move forward while reversing links
            ListNode next = present.next;
            prev = null;

            for (int i = 0; i < k; i++) {
                present.next = prev;   // reverse current link
                prev = present;        // move prev forward
                present = next;        // move present forward
                if (next != null) {
                    next = next.next;
                }
            }

            /*
             After reversal:
             prev     -> head of reversed k-group
             present  -> first node after the reversed group
             newEnd   -> tail of reversed group
            */

            // Step 3: Connect previous part of list to reversed group
            if (last != null) {
                // Reversal does NOT start from head
                last.next = prev;
            } else {
                // Reversal starts from head
                head = prev;
            }

            // Step 4: Connect reversed group with the remaining list
            newEnd.next = present;
           //skip k nodes
            for(int i = 0;present != null && i < k; i++){
            prev = present;
            present = present.next;
        }         
        }

        return head;
    }
}
```
#### Q17) Rotate List:-
- Given the head of a linked list, rotate the list to the right by k places(k = number of rotations).
```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        // Edge cases
        if (head == null || head.next == null || k <= 0) {
            return head;
        }

        // Step 1: Find length and tail
        int length = 1;
        ListNode tail = head;//i.e.last node of original list

        while (tail.next != null) {
            tail = tail.next;
            length++;
        }

        // Step 2: Make it circular, to connect nodes after rotated elements to previous part of list automatically after making newLast.next = null.
        tail.next = head;

        // Step 3: Find new last node
        int rotations = k % length;
        int skip = length - rotations;

        ListNode newLast = head;
        for (int i = 1; i < skip; i++) {
            newLast = newLast.next;
        }

        // Step 4: Break the circle
        head = newLast.next;
        newLast.next = null;

        return head;
    }
}
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```
