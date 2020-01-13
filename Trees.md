## Binary Tree

Node - left pointer, right pointer
Root node

- Linear traversal not possible like in case of Linkedlist. 
- We have two possible directions we can move in (no linear way of traversal possible)

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

**Q4- Sum of nodes of Binary Tree**

**Q5- Structurally Identical**

**Q6- Construct Binary Tree using Inorder and PreOrder**
Inorder sequence: D B E A F C
Preorder sequence: A B D E C F

**Q7- Given a BT, check if it is balancd or not?**

**Q8- Star problem of the day**
**   **
