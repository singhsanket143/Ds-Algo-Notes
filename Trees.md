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
```
