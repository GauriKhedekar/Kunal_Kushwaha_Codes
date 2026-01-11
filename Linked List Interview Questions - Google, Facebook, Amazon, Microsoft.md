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
#### Q5)
