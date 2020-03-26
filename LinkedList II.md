
**Q - You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.**
```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<ListNode*> s1;
        stack<ListNode*> s2;
        ListNode* n1 = l1; ListNode* n2 = l2;
        while(n1 != NULL) {
            s1.push(n1);
            n1 = n1->next;
        }
        while(n2 != NULL) {
            s2.push(n2);
            n2 = n2->next;
        }
        
        int carry = 0;
        ListNode* ans = NULL;
        while(!s1.empty() or !s2.empty()) {
            int val1 = (s1.empty()) ? 0 : s1.top()->val;
            int val2 = (s2.empty()) ? 0 : s2.top()->val;
            int sum = val1 + val2 + carry;
            carry = sum / 10;
            sum = sum % 10;
            if(ans == NULL) {
                ans = new ListNode(sum);
            } else {
                ListNode* temp = new ListNode(sum);
                temp->next = ans;
                ans = temp;
            }
            if(!s1.empty()) s1.pop();
            if(!s2.empty()) s2.pop();
        }
        if(carry!=0) {
            ListNode* temp = new ListNode(carry);
            temp->next = ans;
            ans = temp;
        }
        return ans;
    }
};
```


**Q - Cycle detection in LL**
Explain Hashmap marking approach
Dummy node approach
Floydd Algorithm
Fast pointer can move by doube triple or any higher speed

 **Q- How to detect the start of the loop**
If we have a complete circular LL then the collisiton will occur in n*l cycles

For any LL
dist_small = m + s*l + k
dist_fast = m + f*l

dist_fast = 2*dist_small

then solve the eqn


**Q - Merge Sorted List without space and with space**
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode ans = null;
        ListNode tail = null;
        while(l1 != null && l2 != null){         
            int val1 = l1.val;
            int val2 = l2.val;      
            if(val1 <= val2){
                if(ans == null){
                    ans = l1;
                    tail = l1;  
                }else{
                    tail.next = l1;
                    tail = tail.next;
                }
             l1 = l1.next;
            }else{
                if(ans == null){
                    ans = l2;
                    tail = l2;
                }else{
                    tail.next = l2;
                    tail = tail.next;
                }
                l2 = l2.next;
            }
        }  
        while(l1 != null){
            if(ans == null){
                    ans = l1;
                    tail = l1;
            } else{
                    tail.next = l1;
                    tail = tail.next;
            }
	        l1 = l1.next;
        }
        while(l2 != null){
            if (ans == null){
                    ans = l2;
                    tail = l2;
            } else {
                    tail.next = l2;
                    tail = tail.next;
            }
            l2 = l2.next;
        }
        return ans;
    }
}
```

**Q - Reverse merge sorted listfy**

**Q - Find intersection of 2 lists which have been merged**

Analogy with Array that why LL will be better

**Q- Swap Nodes**

Following cases to be handled. <br>
        1) x and y may or may not be adjacent. <br>
        2) Either x or y may be a head node. <br>
        3) Either x or y may be last node.<br>
        4) x and/or y may not be present in linked list.<br>
            
```java
       
        public void swapNodes(int x, int y) {
         
        // Nothing to do if x and y are same 
        if (x == y) return; 
  
        // Search for x (keep track of prevX and CurrX) 
        Node prevX = null, currX = head; 
        while (currX != null && currX.data != x) 
        { 
            prevX = currX; 
            currX = currX.next; 
        } 
  
        // Search for y (keep track of prevY and currY) 
        Node prevY = null, currY = head; 
        while (currY != null && currY.data != y) 
        { 
            prevY = currY; 
            currY = currY.next; 
        } 
  
        // If either x or y is not present, nothing to do 
        if (currX == null || currY == null) 
            return; 
  
        // If x is not head of linked list 
        if (prevX != null) 
            prevX.next = currY; 
        else //make y the new head 
            head = currY; 
  
        // If y is not head of linked list 
        if (prevY != null) 
            prevY.next = currX; 
        else // make x the new head 
            head = currX; 
  
        // Swap next pointers 
        Node temp = currX.next; 
        currX.next = currY.next; 
        currY.next = temp; 
    } 
        
```
**Q- Swap Nodes in Pairs**

```java
    if(head == null || head.next == null){
            return head;
        }
        ListNode  curr = head.next;
        ListNode prev = head;
        while(head != null && head.next != null){
            
            ListNode first = head;
            ListNode second = head.next;
            prev.next = second;
            first.next = second.next;
            second.next = first;
            
            
            prev = first;
            head = first.next;
        }
        
        return curr;
```
**Q- Flattening a Linked List**
    
```java
    Node flatten(Node root) {
     
        // Base Cases 
        if (root == null || root.right == null) 
            return root; 
  
        // recur for list on right 
        root.right = flatten(root.right); 
  
        // now merge 
        root = merge(root, root.right); 
  
        // return the root 
        // it will be in turn merged with its left 
        return root; 
    } 
    
```

**Q- Flattening a Multilevel Double Linked List**

```java
 if(head == null){
            return head;
        }
            
        Node n = flatten(head.next);
        Node c = flatten(head.child);
        if(c != null){
        head.next = c;
        c.prev = head;
        
        Node temp = c;
        while(temp.next != null){
            temp = temp.next;
        }
        
        temp.next = n;
        if(n != null){    // corner case
        n.prev = temp;
        }
        }
        head.child = null;   // corner case
        return head;

```

**Q- Reverse last K nodes**


**Q- Palindrome**

```java
public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null){
            return true;
        }
        ListNode prev = head;
        ListNode mid = head;
        ListNode fast = head;
        
        while(fast != null && fast.next != null){
            mid = mid.next;
            fast = fast.next.next;
        }
        
        while(prev.next != mid && prev.next != null) {
            prev = prev.next;
        
        }
        
        ListNode n = null;
        if(fast == null){
            n = mid;
            prev.next = null;
        }else{
            n = mid.next;
            mid.next = null;
        }
        
        ListNode second = reverseList(n);
        
        while(second != null && head != null){
            if(second.val != head.val){
                return false;
            }
            second = second.next;
            head = head.next;
        }
        return true;
        
    }
    
    public ListNode reverseList(ListNode head) {
        
        
        ListNode temp = head;
        ListNode prev = null;
        
        
        while(temp != null){
            ListNode fast = temp.next;
            temp.next = prev;
            prev = temp;
            temp = fast;
        }
        
        return prev;
    }
    
}

``` 

**Q- Longest Palindromic Sequence in a LinkedList**
     10 -> 10 -> 2 -> 3 -> 7 -> 3 -> 2 -> 12 -> 20 -> x
```java
static int countCommon(Node a, Node b)  
{  
    int count = 0;  
  
    // loop to count coomon in the list starting  
    // from node a and b  
    for (; a != null && b != null; 
            a = a.next, b = b.next)  
  
        // increment the count for same values  
        if (a.data == b.data)  
            ++count;  
        else
            break;  
  
    return count;  
}  
// Returns length of the longest palindrome sublist in given list  
static int maxPalindrome(Node head)  
{  
    int result = 0;  
    Node prev = null, curr = head;  
  
    // loop till the end of the linked list  
    while (curr != null)  
    {  
        // The sublist from head to current reversed.  
        Node next = curr.next;  
        curr.next = prev;  
  
        // check for odd length palindrome by finding longest common list elements beginning from prev and from next (We exclude curr)  
        result = Math.max(result,  
                    2 * countCommon(prev, next)+1);  
  
        // check for even length palindrome by finding longest common list elements beginning from curr and from next  
        result = Math.max(result,  
                    2*countCommon(curr, next));  
  
        // update prev and curr for next iteration  
        prev = curr;  
        curr = next;  
    }  
    return result;  
}  
```
