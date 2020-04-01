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

**Q2- Left View of Binary Tree**
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
**Q3- Right View of Binary Tree**

Same as before. 
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

**Q4- Lowest Common Ancestor**

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

_Approach 1:_

Find the path of the node p1.
Find the path of the node p2.
Traversal both of the paths till the time path is same. The moment we come across different value in path, the node before it the lowest common ancestor. 

_Approach 2:_

Using backtracking
```java
private TreeNode ans;

    public Solution() {
        // Variable to store LCA node.
        this.ans = null;
    }

    private boolean recurseTree(TreeNode currentNode, TreeNode p, TreeNode q) {

        // If reached the end of a branch, return false.
        if (currentNode == null) {
            return false;
        }

        // Left Recursion. If left recursion returns true, set left = 1 else 0
        int left = this.recurseTree(currentNode.left, p, q) ? 1 : 0;

        // Right Recursion
        int right = this.recurseTree(currentNode.right, p, q) ? 1 : 0;

        // If the current node is one of p or q
        int mid = (currentNode == p || currentNode == q) ? 1 : 0;


        // If any two of the flags left, right or mid become True
        if (mid + left + right >= 2) {
            this.ans = currentNode;
        }

        // Return true if any one of the three bool values is True.
        return (mid + left + right > 0);
    }

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // Traverse the tree
        this.recurseTree(root, p, q);
        return this.ans;
    }
```

**Q5- Path Sum**

![Screenshot 2020-01-15 at 4 53 30 PM](https://user-images.githubusercontent.com/35702912/72430250-dd537b00-37b7-11ea-9a08-15b92b24279d.png)

Path Sum = 22
```java

public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null){
            return false;
        }
       sum = sum - root.val;
       if(root.left == null && root.right == null){
           if(sum == 0){
               return true;
           }else{
               return false;
           }
       }
            
    return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
    }
```

**Q6- Binary Tree Maximum Path Sum**
Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.
```cpp
class Solution {
    
    int globalMax = INT_MIN;
    int maxPathNode2Node(TreeNode* root) {
        // Base case
        if(root == NULL) return 0;
        // Recursive work
        int ls = maxPathNode2Node(root->left); // LST
        int rs = maxPathNode2Node(root->right); // RST
        // Self work
        int cand1 = root->val;
        int cand2 = ls + root->val;
        int cand3 = rs + root->val;
        int cand4 = ls + rs + root->val;
        globalMax = max(cand1, max(cand2, max(cand3, max(cand4, globalMax))));
        return max(ls, max(rs, 0)) + root->val;// My contribution to my parent
    }
}
```


**Star Problem of the day**

_Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment._

_Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure._ 

```java
//Serialize
public String rserialize(TreeNode root, String str) {
    // Recursive serialization.
    if (root == null) {
      str += "null,";
    } else {
      str += str.valueOf(root.val) + ",";
      str = rserialize(root.left, str);
      str = rserialize(root.right, str);
    }
    return str;
  }

  // Encodes a tree to a single string.
  public String serialize(TreeNode root) {
    return rserialize(root, "");
  }

// Deserialize
    if (l.get(0).equals("null")) {
      l.remove(0);
      return null;
    }

    TreeNode root = new TreeNode(Integer.valueOf(l.get(0)));
    l.remove(0);
    root.left = rdeserialize(l);
    root.right = rdeserialize(l);

    return root;
  }

  // Decodes your encoded data to tree.
  public TreeNode deserialize(String data) {
    String[] data_array = data.split(",");
    List<String> data_list = new LinkedList<String>(Arrays.asList(data_array));
    return rdeserialize(data_list);
  }
```

**Homework Problem**

https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/

Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

![Screenshot 2020-01-15 at 5 30 02 PM](https://user-images.githubusercontent.com/35702912/72432301-bc415900-37bc-11ea-9f18-e913f103871a.png)
