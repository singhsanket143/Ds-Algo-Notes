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

## Assignment Questions 

**Q1 - Find the value of nth node from last**
One approach is to find length of LL as L, then . go to L - n + 1 th node

Can we do it in single iteration?
Take two pointers, move one pointer with n distance and then increment both by 1
We need to get something from last, if we look from behind, explain using displacement theory


**Q2- K Reverse**
```java
public void kreverse(int k, Node head) throws Exception {

		LinkedList prev = null;
		LinkedList curr = null;

		while (this.size != 0) {

			curr = new LinkedList();
			for (int i = 1; i <= k; i++) {
				curr.addFirst(this.removeFirst());
			}
			if (prev == null) {
				prev = curr;
			} else {
				prev.tail.next = curr.head;
				prev.tail = curr.tail;
				prev.size = prev.size + curr.size;
			}
		}
		this.head = prev.head;
		this.tail = prev.tail;
		this.size = prev.size;
	}
```




**Q3 - Given a singly linked list  _L_:  _L_0→_L_1→…→_L__n_-1→_L_n,  
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

**Q4- Copy List**

https://leetcode.com/problems/copy-list-with-random-pointer/
