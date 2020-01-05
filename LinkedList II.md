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
**Q- Reverse last K nodes**


**Q- K Reverse**
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
