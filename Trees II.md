**Q1- Serialize and Deserialize Binary Tree**

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

**Q2- Diameter of Binary Tree**

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
**Q3 - Maximum Path Sum**

**Q2- Left View of Binary Tree**

**Q3- Least Common Ancestor**

**Q4- Binary Tree Maximum Path Sum**
 
**Q5- Sum Root to Leaf Numbers**

**Q6- Root to Leaf Paths With Sum**
 
**Q7- Valid Binary Search Tree**
 
**Q8- Path Sum**
 
**Q9- Vertical Order traversal of Binary Tree**
