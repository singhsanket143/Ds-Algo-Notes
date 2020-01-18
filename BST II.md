
### BST AND BT MIXED

**Q1- Longest Consecutive Subsequence in a Binary Tree*

Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

Approach 1: 
1. Total no. of nodes - n
2. Total pair of nodes - nC2 = Total no. of paths
3. Find path between every two nodes and check whether it is increasing or decreasing. 
4. Find the maximum inc/dec out of them. 

Approach 2: 
1. 

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


**Q3- Given a BST, find the kth smallest element in the BST**

Approach 1: Write inorder traversal which will be in sorted form. Then find the kth smallest element.
Approach 2: 

**Q4- Given the preorder traversal of the BST, find the leaf nodes of the BST.**

**Q5- Given a BT, and distance between two nodes, tell the distance between the two nodes.**

**Q6- Given the preorder traversal of a BST, construct the BST out of it.**

**Q7- Target Sum pair in BST**  ( Easy )

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

**Q8- Closest Binary Search Tree Value**  ( Easy )

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

**Q9- Closest Binary Search Tree Value II**     ( Medium )

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
**10- Given a BST, make a BST iterator**

**Q11-  Minimum Cost Tree From Leaf Values**

===============
### Balanced Binary Search Tree

**Q1- Given a BST, convert it into a BBST**


