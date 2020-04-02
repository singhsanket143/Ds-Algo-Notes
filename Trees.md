## Binary Tree

- Covered Linear Data Structure already. Contains a logical start, logical end and a next pointer. 
### Introduction

 
- Hierarchial data structure (Example of Company Hierarchy)
- Relation b/w real tree and computer tree
- Structure of Node
```
class Node{
 int data;
 Node left; 
 Node right;
}
```

- Recursive Data Structure
- We have two possible directions we can move in (no linear way of traversal possible)
- Relationships - Parent-child, sibling, grandfather, root. 
- *Depth* - The depth of a node is the number of edges from the node to the tree's root node.
A root node will have a depth of 0.
- *Height* - The height of a node is the number of edges on the longest path from the node to a leaf.
A leaf node will have a height of 0.

![Screenshot 2020-04-01 at 7 32 20 PM](https://user-images.githubusercontent.com/35702912/78146364-b3713280-744f-11ea-9a90-3c4673f24633.png)

- K Array Tree - Maximum no of child from a node in a tree
- Binary Tree - Two nodes from each child. 
 
### Application

 - File system components
 - Decision Tree
 - Tries
 - URL lookups
 
### Properties

1) The maximum number of nodes at level ‘l’ of a binary tree is 2^(l-1).

2) Maximum number of nodes in a binary tree of height ‘h’ is 2^h – 1.

### Types of Trees


- _Full Binary Tree_: A Binary Tree is full if every node has 0 or 2 children. 

- _Complete Binary Tree:_ A Binary Tree is complete Binary Tree if all levels are completely filled except possibly the last level and the last level has all keys as left as possible

- _Perfect Binary Tree:_ A Binary tree is Perfect Binary Tree in which all internal nodes have two children and all leaves are at the same level.
 

### Traversal

- Preorder    NLR
- Inorder     LNR
- Postorder   LRN

## Assignment Problems

**Q1- Inorder**

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

```java


//  Preorder Iteratively Algo

1) Create an empty stack nodeStack and push root node to stack.
2) Do following while nodeStack is not empty.
….a) Pop an item from stack and print it.
….b) Push right child of popped item to stack
….c) Push left child of popped item to stack


```
**Q2- Construct Binary Tree using Inorder and PreOrder**

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

**Q3- Check if given Preorder, Inorder and Postorder traversals are of same tree**


*Another type of Traversal*
**Q4- LevelOrder Traversal**

```java

 
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
**Q5- Vertical Order traversal of Binary Tree**

**Approach 1:**


The idea is to traverse the tree once and get the minimum and maximum horizontal distance with respect to root. For the tree shown above, minimum distance is -2 (for node with value 2) and maximum distance is 2 (For node with value 9).

Once we have maximum and minimum distances from root, we iterate for each vertical line at distance minimum to maximum from root, and for each vertical line traverse the tree and print the nodes which lie on that vertical line.
Given a binary tree, return the vertical order traversal of its nodes values.

```java

//PseudoCode

// min --> Minimum horizontal distance from root
// max --> Maximum horizontal distance from root
// hd  --> Horizontal distance of current node from root 

findMinMax(tree, min, max, hd)
     if tree is NULL then return;
 
     if hd is less than min then
           min = hd;
     else if hd is greater than max then
          *max = hd;
 
     findMinMax(tree->left, min, max, hd-1);
     findMinMax(tree->right, min, max, hd+1);

 
printVerticalLine(tree, line_no, hd)
     if tree is NULL then return;
 
     if hd is equal to line_no, then
           print(tree->data);
     printVerticalLine(tree->left, line_no, hd-1);
     printVerticalLine(tree->right, line_no, hd+1); 
     

void verticalOrder(Node node)  { 
        findMinMax(node, val, val, 0); 
        for (int line_no = val.min; line_no <= val.max; line_no++)  
        { 
            printVerticalLine(node, line_no, 0); 
            System.out.println(""); 
        } 
    } 

```

*Time Complexity:*

Time complexity of above algorithm is O(w*n) where w is width of Binary Tree and n is number of nodes in Binary Tree. 

In worst case, the value of w can be O(n) (consider a complete tree for example) and time complexity can become O(n^2).

**Approach 2:**

We need to check the Horizontal Distances from the root for all nodes. If two nodes have the same Horizontal Distance (HD), then they are on the same vertical line. The idea of HD is simple. HD for root is 0, a right edge (edge connecting to right subtree) is considered as +1 horizontal distance and a left edge is considered as -1 horizontal distance. 

We can do preorder traversal of the given Binary Tree. While traversing the tree, we can recursively calculate HDs. We initially pass the horizontal distance as 0 for root. 

For left subtree, we pass the Horizontal Distance as Horizontal distance of root minus 1. 

For right subtree, we pass the Horizontal Distance as Horizontal Distance of root plus 1. For every HD value, we maintain a list of nodes in a hash map. Whenever we see a node in traversal, we go to the hash map entry and add the node to the hash map using HD as a key in a map.

```java
static void getVerticalOrder(Node root, int hd, 
                                TreeMap<Integer,Vector<Integer>> m) 
    { 
        // Base case 
        if(root == null) 
            return; 
          
        //get the vector list at 'hd' 
        Vector<Integer> get =  m.get(hd); 
          
        // Store current node in map 'm' 
        if(get == null) 
        { 
            get = new Vector<>(); 
            get.add(root.key); 
        } 
        else
            get.add(root.key); 
          
        m.put(hd, get); 
          
        // Store nodes in left subtree 
        getVerticalOrder(root.left, hd-1, m); 
          
        // Store nodes in right subtree 
        getVerticalOrder(root.right, hd+1, m); 
    } 
      
    // The main function to print vertical order of a binary tree 
    // with the given root 
    static void printVerticalOrder(Node root) 
    { 
        // Create a map and store vertical order in map using 
        // function getVerticalOrder() 
        TreeMap<Integer,Vector<Integer>> m = new TreeMap<>(); 
        int hd =0; 
        getVerticalOrder(root,hd,m); 
          
        // Traverse the map and print nodes at every horigontal 
        // distance (hd) 
        for (Entry<Integer, Vector<Integer>> entry : m.entrySet()) 
        { 
            System.out.println(entry.getValue()); 
        } 
    } 
```

Time Complexity: O(n)

Space Complexity: O(n)

**Codechef - Joker vs Batman**

https://www.codechef.com/problems/CDIT04

- Trees

## Homework Problems

**Q- LevelOrder Linewise**
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

**Q1- LeverOrder Linewise ZigZag**
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
