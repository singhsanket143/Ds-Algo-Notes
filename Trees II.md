## Theory type Questions

**Q- Height of Binary Tree**

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

**Q- Find a element in Binary Tree**

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

**Q- Sum of nodes of Binary Tree**

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

## Assignment Problems

**Q1- Diameter of Binary Tree**

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

_Approach 1:_

```java
public int diameterOfBinaryTree(TreeNode root) {
        if(root == null){
            return 0;
        }
        
        int left = diameterOfBinaryTree(root.left);
        int right = diameterOfBinaryTree(root.right);
        
        int self = height(root.left) + height(root.right) + 2;
        
        return Math.max(left, Math.max(right, self));
        
    }
    
    public int height(TreeNode root){
        if(root == null){
            return -1;
        }
        
        int left = height(root.left);
        int right = height(root.right);
        
        return Math.max(left, right) + 1;
    }
```

Approach 2: 

```java
public class Diapair{
        int diameter;
        int height;
    }
    public Diapair diameter(TreeNode root){
         if(root == null){
            Diapair base = new Diapair();
            base.height = -1;
            base.diameter = 0;
             return base;
        }
    
        Diapair left = diameter(root.left);
        Diapair right = diameter(root.right);
        
        Diapair self = new Diapair();
        self.height = Math.max(left.height, right.height) + 1;
        
        self.diameter = Math.max(left.diameter, Math.max(right.diameter, left.height + right.height + 2)) ;
        return self;
        
    }
    public int diameterOfBinaryTree(TreeNode root) {
       return diameter(root).diameter;
    }
```

**Q2- Given a BT, check if it is balanced or not?**

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

**Q3- Top View of Binary Tree**

https://www.geeksforgeeks.org/print-nodes-in-top-view-of-binary-tree-set-2/
Given a binary tree, print the top view of it. The output nodes should be printed from left to right.

**Q4- Right View of Binary Tree**

```java
public List<Integer> rightSideView(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<>();
        if(root == null){
            return list;
        }
        Queue<TreeNode> primary = new LinkedList<>();
        Queue<TreeNode> helper = new LinkedList<>();
        primary.add(root);
        list.add(root.val);
        while(!primary.isEmpty()){
            
            TreeNode node = primary.remove();
            if(node.right != null){
                helper.add(node.right);
            }
            if(node.left != null){
                helper.add(node.left);
            }
            if(primary.isEmpty()){
                if(!helper.isEmpty()){
                list.add(helper.element().val);
                primary = helper;
                helper = new LinkedList<>();
                }
            }
        }
        return list;
    }
```

**Q5**

_Given a binary tree_

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


https://leetcode.com/problems/populating-next-right-pointers-in-each-node/solution/

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


**Homework Problems**

**Q- Structurally Identical**

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


**Q3- Left View of Binary Tree**

```java
static void leftViewUtil( node root ) 
{ 
    if (root == null) 
        return;
    q.add(root); 

    q.add(null); 
  
    while (q.size() > 0)  
    { 
        node temp = q.peek(); 
        if (temp != null) 
        { 
            System.out.print(temp.data + " ");
            while (q.peek() != null) 
            { 
                if (temp.left != null) 
                    q.add(temp.left); 
  
                if (temp.right != null) 
                    q.add(temp.right); 
                q.remove(); 
                temp = q.peek(); 
            } 
            q.add(null); 
        }  
        q.remove(); 
    } 
} 

```

## Extra Problem

https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/

Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

![Screenshot 2020-01-15 at 5 30 02 PM](https://user-images.githubusercontent.com/35702912/72432301-bc415900-37bc-11ea-9f18-e913f103871a.png)

