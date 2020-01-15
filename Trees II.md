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
**Q4- Right View of Binary Tree**

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

**Q5- Lowest Common Ancestor**

**Q6- Path Sum**


![Screenshot 2020-01-15 at 4 53 30 PM](https://user-images.githubusercontent.com/35702912/72430250-dd537b00-37b7-11ea-9a08-15b92b24279d.png)

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

**Q7- Path Sum**
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

**Q4- Binary Tree Maximum Path Sum**

 
**Q5- Sum Root to Leaf Numbers**

**Q6- Root to Leaf Paths With Sum**
 

 
**Q9- Vertical Order traversal of Binary Tree**

**Q10 - Maximum Width of Binary Tree**
**Q3 - Maximum Path Sum**
