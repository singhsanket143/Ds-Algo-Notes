## Binary Tree
### Introduction
- Recursive Data Structure
- Hierarchial data structure
- Linear traversal not possible like in case of Linkedlist. 
- We have two possible directions we can move in (no linear way of traversal possible)
- Relationships - Parent-child, sibling, grandfather, root. 

### Application
 - File system components
 - Decision Tree
 - Tries
 - URL lookups
 
### Properties
1) The maximum number of nodes at level ‘l’ of a binary tree is 2^(l-1).

2) Maximum number of nodes in a binary tree of height ‘h’ is 2h – 1.

### Types of Trees

- _Full Binary Tree_ A Binary Tree is full if every node has 0 or 2 children. 
- _Complete Binary Tree:_ A Binary Tree is complete Binary Tree if all levels are completely filled except possibly the last level and the last level has all keys as left as possible
- A binary tree is _balanced_ if the height of the tree is O(Log n) where n is the number of nodes. For Example, AVL tree maintains O(Log n) height by making sure that the difference between heights of left and right subtrees is atmost 1. 
A degenerate (or pathological) tree A Tree where every internal node has one child. Such trees are performance-wise same as linked list.
### Traversal
- Inorder     LNR
- Postorder   LRN
- Preorder    NLR
- Level order 

Time Complexity : O(n)
Space Complexity: O(n)


```java
//Recursion

inorder(Node root){
  if(root == null){
  return;
  }
  
  inorder(root.left);
  print(root.val);
  inroder(root.right);
}

//Iterative

void inorder() 
    { 
        if (root == null) 
            return; 
        Stack<Node> s = new Stack<Node>(); 
        Node curr = root; 

        while (curr != null || s.size() > 0) 
        { 
            while (curr !=  null) 
            { 
                s.push(curr); 
                curr = curr.left; 
            } 
            curr = s.pop(); 
  
            System.out.print(curr.data + " "); 
            curr = curr.right; 
        }
     }
 
 // LevelOrder
 
 public void LevelOrder() {

		LinkedList<Node> queue = new LinkedList<>();
		queue.addLast(this.root);

		while (!queue.isEmpty()) {

			Node rn = queue.removeFirst();
			System.out.println(rn.data);

			if (rn.left != null)
				queue.add(rn.left);

			if (rn.right != null)
				queue.add(rn.right);
		}

	}
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q1- LevelOrder Linewise**
```java
private void levelorderLineWise(Node node) {

		LinkedList<Node> primaryq = new LinkedList<>();
		LinkedList<Node> helperq = new LinkedList<>();

		primaryq.addLast(node);

		while (!primaryq.isEmpty()) {

			Node pp = primaryq.removeFirst();
			System.out.print(pp.data + " ");

			if (pp.left != null)
				helperq.addLast(pp.left);

			if (pp.right != null)
				helperq.addLast(pp.right);

			if (primaryq.size() == 0) {
				System.out.println();
				primaryq = helperq;
				helperq = new LinkedList<>();
			}

		}
	}
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q2- LeverOrder Linewise ZigZag**
```java
public void levelorderZigZag() {

		LinkedList<Node> queue = new LinkedList<>();
		LinkedList<Node> stack = new LinkedList<>();

		queue.add(this.root);
		int count = 0;

		while (!queue.isEmpty()) {

			Node pp = queue.removeFirst();
			System.out.print(pp.data + " ");

			if (count % 2 == 0) {

				if (pp.left != null)
					stack.addFirst(pp.left);
				if (pp.right != null)
					stack.addFirst(pp.right);
			}

			else {

				if (pp.right != null)
					stack.addFirst(pp.right);
				if (pp.left != null)
					stack.addFirst(pp.left);

			}

			if (queue.size() == 0) {

				count++;
				queue = stack;
				stack = new LinkedList<>();
			}
		}

	}
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q3- Height of Binary Tree**
```java
private int height(Node node) {

		if (node == null) { // base case
			return -1;
		}

		int lh = height(node.left);
		int rh = height(node.right);

		return Math.max(lh, rh) + 1;
	}

```
Time Complexity: O(n)
Space Complexity: O(n)

**Q4- Find a element in Binary Tree**
```java
private boolean find(Node node, int item) {

		if (node == null) {
			return false;
		}

		if (node.data == item)
			return true;

		boolean lresult = find(node.left, item);

		if (lresult) {
			return true;
		}

		boolean rresult = find(node.right, item);

		if (rresult) {
			return true;
		}

		return false;
	}
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q5- Sum of nodes of Binary Tree**
```java
private int sumofnodes(Node node) {

		if (node == null)
			return 0;

		int lsum = sumofnodes(node.left);
		int rsum = sumofnodes(node.right);

		return lsum + rsum + node.data;

	}
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q6- Structurally Identical**
```java
private boolean structurallyIdentical(Node tnode, Node onode) {

		if (tnode == null && onode == null) {
			return true;
		}
		if (tnode == null || onode == null) {
			return false;
		}

		boolean l = structurallyIdentical(tnode.left, onode.left);
		boolean r = structurallyIdentical(tnode.right, onode.right);

		return l && r;
	}
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q7- Construct Binary Tree using Inorder and PreOrder**
Inorder sequence: D B E A F C
Preorder sequence: A B D E C F
```java
private Node construct(int[] pre, int[] in, int plo, int phi, int ilo, int ihi) {

		if (plo > phi) { // base case
			return null;
		}
		// make a new node
		Node nn = new Node();
		nn.data = pre[plo]; // first node of preorder array will be root node
		// increment size
		this.size++;
		int s = -1;
		// search the node in inorder array
		for (int i = ilo; i <= ihi; i++) {

			if (pre[plo] == in[i]) {
				s = i;
				break;
			}
		}

		int a = s - ilo;
		// node left
		nn.left = construct(pre, in, plo + 1, plo + a, ilo, s - 1);
		// node right
		nn.right = construct(pre, in, plo + a + 1, phi, s + 1, ihi);

		return nn;

	}
```
Time Complexity: O(n)
Space Complexity: O(n)


**Q8- Given a BT, check if it is balanced or not?**
```java
private class BalancePair {

		int height;
		boolean isBalanced;

	}

	public boolean isBalanced() {

		return this.isBalanced(this.root).isBalanced;
	}

	private BalancePair isBalanced(Node node) {

		if (node == null) {

			BalancePair bp = new BalancePair();
			bp.height = -1;
			bp.isBalanced = true;
			return bp;
		}

		BalancePair lbp = isBalanced(node.left);
		BalancePair rbp = isBalanced(node.right);

		int lh = lbp.height;
		int rh = rbp.height;

		BalancePair mp = new BalancePair();

		mp.height = Math.max(lh, rh) + 1;

		if (Math.abs(lh - rh) <= 1 && lbp.isBalanced && rbp.isBalanced) {

			mp.isBalanced = true;

		} else {

			mp.isBalanced = false;
		}
		return mp;
	}
```
Time Complexity: O(n)
Space Complexity: O(n)


**Q9- Merge two binary trees**

```java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null && t2 == null) return null;
        
        if(t2 == null) return t1;
        if(t1 == null) return t2;
        
        TreeNode left = mergeTrees(t1.left, t2.left);
        TreeNode right = mergeTrees(t1.right, t2.right);
        
        TreeNode result = new TreeNode(t1.val + t2.val);
        
        result.left = left;
        result.right = right;
        return result;
    }
}
```

Time Complexity: O(n)
Space Complexity: O(n)

**Q10- Invert Binary Tree**

```java
	public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return null;   
        }
        TreeNode left = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        
        root.right = left;
        root.left = right;
        
        return root;
    }

```
Time Complexity: O(n)
Space Complexity: O(n)


**Q11- Star problem of the day**
Given a binary tree
```java
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}

```
**Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.**

**Initially, all next pointers are set to NULL.**

_Approach 1_:
```java
public Node connect(Node root) {
        
        if (root == null) {
            return root;
        }
        
        // Initialize a queue data structure which contains
        // just the root of the tree
        Queue<Node> Q = new LinkedList<Node>(); 
        Q.add(root);
        
        // Outer while loop which iterates over 
        // each level
        while (Q.size() > 0) {
            
            // Note the size of the queue
            int size = Q.size();
            
            // Iterate over all the nodes on the current level
            for(int i = 0; i < size; i++) {
                
                // Pop a node from the front of the queue
                Node node = Q.poll();
                
                // This check is important. We don't want to
                // establish any wrong connections. The queue will
                // contain nodes from 2 levels at most at any
                // point in time. This check ensures we only 
                // don't establish next pointers beyond the end
                // of a level
                if (i < size - 1) {
                    node.next = Q.peek();
                }
                
                // Add the children, if any, to the back of
                // the queue
                if (node.left != null) {
                    Q.add(node.left);
                }
                if (node.right != null) {
                    Q.add(node.right);
                }
            }
        }
        
        // Since the tree has now been modified, return the root node
        return root;
    }

```

_Approach 2:_

Intuition

```java
leftmost = root
 while (leftmost.left != null)
 {
     head = leftmost
     while (head.next != null)
     {
         1) Establish Connection 1
         2) Establish Connection 2 using next pointers
         head = head.next
     }
     leftmost = leftmost.left
 }

```
Code: 
```java

 Node prev, leftmost;
    
    public void processChild(Node childNode) {
        
        if (childNode != null) {
            if (this.prev != null) {
                this.prev.next = childNode;
                    
            } else {
                
                this.leftmost = childNode;
            }    
                
            this.prev = childNode; 
        }
    }
        
    public Node connect(Node root) {
        
        if (root == null) {
            return root;
        }
        
        this.leftmost = root;
        
     
        Node curr = leftmost;
        
      
        while (this.leftmost != null) {
        
            this.prev = null;
            curr = this.leftmost;
            
            this.leftmost = null;
        
            while (curr != null) {
         
                this.processChild(curr.left);
                this.processChild(curr.right);
                
                curr = curr.next;
            }
        }
                
        return root ;
    }
```

Time Complexity: O(n)
Space Complexity: O(1)


**Codechef - Joker vs Batman**

https://www.codechef.com/problems/CDIT04
