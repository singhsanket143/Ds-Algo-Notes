## Binary Tree
### Introduction
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
1) The maximum number of nodes at level ‘l’ of a binary tree is 2l-1.

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

**Q1- LevelOrder Linewise**

**Q2- LeverOrder Linewise ZigZag**

**Q3- Height of Binary Tree**

**Q4- Find a element in Binary Tree**

**Q5- Sum of nodes of Binary Tree**

**Q6- Structurally Identical**

**Q7- Construct Binary Tree using Inorder and PreOrder**
Inorder sequence: D B E A F C
Preorder sequence: A B D E C F

**Q8- Given a BT, check if it is balancd or not?**

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
**Q10- Invert Binary Tree**

**Q11- Star problem of the day**


