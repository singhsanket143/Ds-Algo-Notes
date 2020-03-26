# Linked List

- LinkedList donot have index based access
- Arrays have index based access

**Pros n Cons**

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

**Q- Reverse the LinkedList**

  - Discuss all four approaches
    
  _Pointer Iteratively_
    
```java
    
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
```
   _Data Iteratively_
    
```java
   public Node reverseList(ListNode head) {

		if (this.size == 0) {
			throw new Exception("LL is empty");
		}

		for (int i = 0; i < this.size / 2; i++) { // O(n/2)

			Node n1 = getNodeAt(i); // O(n)
			Node n2 = getNodeAt(this.size - i - 1);

			int temp = n1.data; // swap
			n1.data = n2.data;
			n2.data = temp;

		}

	}
```
    
  _Pointer Recursively_
   
```java
    public void Reverse_PR() throws Exception {

		if (this.size == 0) {
			throw new Exception("LL is empty");
		}

		RPH(this.head, this.head.next);

		Node temp = this.head; // swap tail and head
		this.head = this.tail;
		this.tail = temp;
		this.tail.next = null;

	}

	private void RPH(Node prev, Node curr) {

		if (curr == null) { // base case
			return;
		}

		RPH(prev.next, curr.next);
		curr.next = prev;

	}
    
```
   _Data Recursively_
```java
    public void Reverse_RD() throws Exception {

		if (this.size == 0) {
			throw new Exception("LL is empty");
		}

		Heapmover left = new Heapmover();
		left.node = this.head;

		RDH(left, this.head, 0);

	}

	public void RDH(Heapmover left, Node right, int count) {

		if (right == null) {
			return;
		}

		RDH(left, right.next, count + 1);

		if (count >= this.size / 2) {

			int temp = left.node.data; // swapping of data
			left.node.data = right.data;
			right.data = temp;
		}

		left.node = left.node.next;

	}
    
```
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

## Homework Problems

**Q1- Find mid node in LL**
Approach 1 -> calculate length then again traverse length/2 distance
Approach 2 ->Mid point is at distance 'd' and end point is at distance '2d'

**Q4 - Given a linked list, swap every two adjacent nodes and return its head. You may  not  modify the values in the list's nodes, only nodes itself may be changed.**
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



