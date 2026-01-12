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
#### Q9) 
