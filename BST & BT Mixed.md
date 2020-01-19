
### BST AND BT MIXED

**Q1- Longest Consecutive Subsequence in a Binary Tree*

Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.               

![Screenshot 2020-01-19 at 5 29 42 PM](https://user-images.githubusercontent.com/35702912/72680571-59fc9700-3ae1-11ea-8d81-9ed10d6f8178.png)
Output: 4

Approach 1: 
1. Total no. of nodes - n
2. Total pair of nodes - nC2 = Total no. of paths
3. Find path between every two nodes and check whether it is increasing or decreasing. 
4. Find the maximum inc/dec out of them. 

Approach 2: 

```java

 int result = 0;
    public class Pair{
        int inc;
        int dec;
    }
    public int longestConsecutive(TreeNode root) {
        helper(root);
        return result;
        
    }
    
    public Pair helper(TreeNode root){
        if(root == null){
            Pair p = new Pair();
            p.inc = 0;
            p.dec = 0;
            return p;
        }
        int inc = 1;
        int dec = 1;
        Pair left = helper(root.left);
        Pair right = helper(root.right);
        
        Pair mypair  = new Pair();
        
        if(root.left != null){   
            if(root.val == root.left.val + 1){
                
                dec += left.dec;
            }
            if(root.val == root.left.val - 1){
                
                inc += left.inc;
            }
        }
        if(root.right != null){
            if(root.val == root.right.val + 1){
                
                dec = Math.max(dec, right.dec + 1);
            }
            if(root.val == root.right.val - 1){
        
                inc = Math.max(inc, right.inc + 1);
            }
        }
        
        result = Math.max(inc + dec - 1, result);
        mypair.dec = dec;
        mypair.inc = inc;
        return mypair;
    }
```

Time Complexity: O(n)

Space Complexity: O(n)

**Q2- Cousins in Binary Tree** 

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.
Two nodes of a binary tree are cousins if they have the same depth, but have different parents.
We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.
Return true if and only if the nodes corresponding to the values x and y are cousins.

![Screenshot 2020-01-18 at 10 53 52 PM](https://user-images.githubusercontent.com/35702912/72667771-6f23e800-3a45-11ea-94de-c74d80e95a2c.png)

```java
 Map<Integer, Integer> depth;
    Map<Integer, TreeNode> parent;
    public boolean isCousins(TreeNode root, int x, int y) {
        depth = new HashMap<>();
        parent = new HashMap<>();
        dfs(root, null);
        return (depth.get(x) == depth.get(y) && parent.get(x) != parent.get(y));
        
    }
    
    public void dfs(TreeNode node, TreeNode par){
        if(node == null){
            return;
        }
        depth.put(node.val, par != null ? 1 + depth.get(par.val): 0);
        parent.put(node.val, par);
        dfs(node.left, node);
        dfs(node.right, node);
    }
    

```

Time Complexity: O(n)

Space Complexity: O(n)


**Q3- Given the preorder traversal of the BST, find the leaf nodes of the BST.**

![Screenshot 2020-01-19 at 1 13 17 AM](https://user-images.githubusercontent.com/35702912/72669537-e616ac00-3a58-11ea-9036-822937838aa1.png)

_Approach 1:_

The idea is to use two min and max variables and taking i (index in input array), the index for given preorder array, and recursively creating root node and correspondingly checking if left and right are existing or not. This method return boolean variable, and if both left and right are false it simply means that left and right are null hence it must be a leaf node so print it right there and return back true as root at that index existed.

```java
static int i = 0; 
  
    // Print the leaf node from the given preorder of BST. 
    static boolean isLeaf(int pre[], int n, 
            int min, int max) 
    { 
        if (i >= n) 
        { 
            return false; 
        } 
  
        if (pre[i] > min && pre[i] < max)  
        { 
            i++; 
  
            boolean left = isLeaf(pre, n, min, pre[i - 1]); 
            boolean right = isLeaf(pre, n, pre[i - 1], max); 
  
            if (!left && !right)  
            { 
                System.out.print(pre[i - 1] + " "); 
            } 
  
            return true; 
        } 
        return false; 
    } 
```
Time Complexity: O(n)

Space Complexity: O(n)

**Q4- Given a BT, and two nodes, tell the distance between the two nodes.**

Approach 1: Using LCA
```
  Dist(n1, n2) = Dist(root, n1) + Dist(root, n2) - 2*Dist(root, lca) 
  'n1' and 'n2' are the two given keys
  'root' is root of given Binary Tree.
  'lca' is lowest common ancestor of n1 and n2
  Dist(n1, n2) is the distance between n1 and n2.

```

Time Complexity: O(n)

Space Complexity: O(n)

Approach 2: Find LCA of two nodes. Then, find distance from LCA to two nodes.

Time Complexity: O(n)

Space Complexity: O(n)


**Q5- Given the preorder traversal of a BST, construct the BST out of it.**


```java
  int idx = 0;
  int[] preorder;
  int n;

  public TreeNode helper(int lower, int upper) {
    // if all elements from preorder are used then the tree is constructed
    if (idx == n) return null;

    int val = preorder[idx];
    // if the current element couldn't be placed here to meet BST requirements
    if (val < lower || val > upper) return null;

    // place the current element and recursively construct subtrees
    idx++;
    TreeNode root = new TreeNode(val);
    root.left = helper(lower, val);
    root.right = helper(val, upper);
    return root;
  }

  public TreeNode bstFromPreorder(int[] preorder) {
    this.preorder = preorder;
    n = preorder.length;
    return helper(Integer.MIN_VALUE, Integer.MAX_VALUE);
  }
```

Time Complexity: O(n)

Space Complexity: O(n)


**Q6- Target Sum pair in BST**  ( Easy )

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

![Screenshot 2020-01-18 at 10 39 49 PM](https://user-images.githubusercontent.com/35702912/72667591-73e79c80-3a43-11ea-8843-430bb6c15421.png)

```java

public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet();
        return find(root, k, set);
    }
    
    public boolean find(TreeNode root, int k, Set<Integer> s){
        if(root == null){
            return false;
        }
        
        boolean left = find(root.left, k, s);
        int val = root.val;
        if(s.contains(k-val)){
            return true;
        }else{
            s.add(val);
        }
        
        boolean right = find(root.right, k, s);
        return right || left;
    }
```
Time Complexity: O(n)

Space Complexity: O(n)

**Q7- Closest Binary Search Tree Value**  ( Easy )

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

![Screenshot 2020-01-18 at 8 45 52 PM](https://user-images.githubusercontent.com/35702912/72665979-9c679a80-3a33-11ea-8bec-185de291c86e.png)
```java

public int closestValue(TreeNode root, double target) {
            
        int val, closest = root.val;
        while (root != null) {
        val = root.val;
        closest = Math.abs(val - target) < Math.abs(closest - target) ? val : closest;
        root =  target < root.val ? root.left : root.right;
        }
    return closest;
    }
```

Time Complexity: O(H)

Space Complexity: O(1)

**Q8- Closest Binary Search Tree Value II**     ( Medium )

Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

Input: _Same Tree as before._

k = 2

Output: [4, 3]

```java
public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> list = new ArrayList<>();
        
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();
        
        inorder(root, target, false, s1);
        inorder(root, target, true, s2);
        
        while(k-- > 0){
            if(s1.isEmpty()){
                list.add(s2.pop());
            }else if(s2.isEmpty()){
                list.add(s1.pop());
            }else{
                if(Math.abs(s1.peek() - target) < Math.abs(s2.peek() - target)){
                    list.add(s1.pop());
                }else{
                    list.add(s2.pop());
                }
            }
        }
        
        return list;
        
    }
    
    public void inorder(TreeNode root, double target, boolean reverse, Stack<Integer> s){
        if(root == null){
            return;
        }
        
        inorder(reverse? root.right: root.left, target, reverse, s);
        if(reverse && root.val <= target || !reverse && root.val > target){
            return;
        }
        s.push(root.val);
        inorder(reverse? root.left: root.right, target, reverse, s);
    }
```

Time Complexity: O(n)

Space Complexity: O(n)

**Q9-  Minimum Cost Tree From Leaf Values**

Given an array arr of positive integers, consider all binary trees such that:

Each node has either 0 or 2 children;
The values of arr correspond to the values of each leaf in an in-order traversal of the tree.  (Recall that a node is a leaf if and only if it has 0 children.)
The value of each non-leaf node is equal to the product of the largest leaf value in its left and right subtree respectively.
Among all possible binary trees considered, return the smallest possible sum of the values of each non-leaf node.  It is guaranteed this sum fits into a 32-bit integer.

![Screenshot 2020-01-19 at 1 58 26 AM](https://user-images.githubusercontent.com/35702912/72670080-4c063200-3a5f-11ea-9714-f2fd63f6cb66.png) 


