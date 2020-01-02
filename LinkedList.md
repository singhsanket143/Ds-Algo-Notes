# Linked List
- Tribe example for explaining linked list
- Non-Linear Data Structure
	- in order to get to the end of the list, we have to go through all of the items in the list in order, or sequentially
- LinkedList donot have index based access
- Arrays have index based access

**Advantages**
- Array give random access but LL dont. 
- Lesser storage required for arrays because ll also stores pointers
- insertions in between nodes is easy in LL whereas insertion in between positions of array is difficult

### Linked list structure
```cpp
class Node {
	public:
	int data;
	Node *next
};
```
**Time Complexity of Operations in LinkedList**

- Insertion 
	- At front O(1)
	- At end O(n) 
	- At Middle O(k) ( Addition after kth Node)
- Deletion
	- At front O(1)
	- At end O(n) ( If tail not present )
	- At Middle O(k) ( Addition after kth Node)

- Traversal
  	- O(n)

*Essential feature to know in the LL is head**


**Q - How to delete the complete list if we know the head??**
In Java just delete the head, but in C or C++ there is no auto garbage collection, we will iteratively delete the nodes

**Q - Find the value of nth node from first**
Just iterate from head till n iterations

**Q - Find the value of nth node from last**
One approach is to find length of LL as L, then . go to L - n + 1 th node

Can we do it in single iteration?
Take two pointers, move one pointer with n distance and then increment both by 1
We need to get something from last, if we look from behind, explain using displacement theory

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

**Q - Find mid node in LL**
Approach 1 -> calculate length then again traverse length/2 distance
Approach 2 ->Mid point is at distance 'd' and end point is at distance '2d'

Q - Search in LL
Q - Discuss Skip List

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
**Q - Given a linked list, swap every two adjacent nodes and return its head. You may  not  modify the values in the list's nodes, only nodes itself may be changed.**
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
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
     }
}
```
**Q - Given a singly linked list  _L_:  _L_0→_L_1→…→_L__n_-1→_L_n,  
reorder it to:  _L_0→_L__n_→_L_1→_L__n_-1→_L_2→_L__n_-2→… 
You may not  modify the values in the list's nodes, only nodes itself may be changed.**
```java
class Solution {  
    public class Heapmover {
		ListNode node;
	}
    public void reorderList(ListNode head) {   
        Heapmover left = new Heapmover();
		left.node = head;
        int count = 0;
        ListNode temp = head;
        while(temp != null){
            temp = temp.next;
            count++;
        }
		this.fold(left, head, 0, count);   
    }
	public void fold(Heapmover left, ListNode right, int counter, int size) {
		if (right == null) {
			return;
		}
		fold(left, right.next, counter + 1, size);
		if (counter > size / 2) {
			ListNode temp = left.node.next;
			left.node.next = right;
			right.next = temp;
			left.node = temp;
		}
		if (counter == size / 2) {	
			right.next = null;
		}
	}
}
```
- Approach 2 -> 
1) Find middle of LL
2) Reverse the half after middle
3) Start reordering one by one
