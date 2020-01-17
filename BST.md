**Binary Search Tree**
- Extension of Binary Tree
- All nodes in left subtree will be smaller than root.
- All nodes in right subtree will be greater than root.
- Inorder traversal yields sorted ordering of the element

**How to handle equal elements?**

- Either keep a count on every node
- Same elements can either go in left or right subtree

**Delete a node in BST**
```java
public void remove(int item) {

		remove(this.root, null, false, item);
	}

	private void remove(Node node, Node parent, boolean ilc, int item) {

		if (node == null) {
			return;
		}
		if (item < node.data) {

			remove(node.left, node, true, item);
		} else if (item > node.data) {

			remove(node.right, node, false, item);
		} else {

			if (node.left == null && node.right == null) {
				if (ilc)
					parent.left = null;
				else
					parent.right = null;

			} else if (node.left != null && node.right == null) {
				if (ilc)
					parent.left = node.left;
				else
					parent.right = node.left;
				this.size--;
			} else if (node.right != null && node.left == null) {
				if (ilc)
					parent.left = node.right;
				else
					parent.right = node.right;
				this.size--;
			} else {

				int max = max(node.left);
				node.data = max;

				remove(node.left, node, true, max);

			}
		}
```
**Add a node in BST**

```java
public void add(int item) {

		add(this.root, null, false, item);
	}

	private void add(Node node, Node parent, boolean ilc, int item) {

		if (node == null) { // base case

			Node nn = new Node();
			nn.data = item;
			this.size++;
			if (ilc)
				parent.left = nn;
			else
				parent.right = nn;

			return;
		}
		if (item < node.data) {

			add(node.left, node, true, item);
		}
		if (item > node.data) {
			add(node.right, node, false, item);
		}
	}
```
**Q1- Print in Range**
```java
public void printInRange(int lower, int upper) {

		printInRange(this.root, lower, upper);

	}
	private void printInRange(Node node, int lower, int upper) {
		if (node == null) {
			return;
		}

		if (node.data > upper) {
			printInRange(node.left, lower, upper);
		}

		else if (node.data < lower) {
			printInRange(node.right, lower, upper);
		}

		else {

			printInRange(node.left, lower, upper);
			System.out.println(node.data);
			printInRange(node.right, lower, upper);
		}

	}
```
**Q2- Check if a given BT is BST**
Approach1: Write inorder traversal
Approach2: 3 conditions:
- left subtree is a BST
- right subtree is a BST
- root is greater than the max value in left subtree
- root is less than the lowest value in right subtree

**Q3- Given a BST, find the kth smallest element in the BST**

**Q4- Largest Binary Search Tree in BT**

**Q5- Given a BST, somebody swapped 2 elements, Find out which pair was swapped?**

_Trivial Approach_

- Take inorder of the given tree
- Copy the inorder in a different array and sort it 
- The indexes with different values gives us sorted elements

Intuition - Had it been a perfect bst, both the array would be having same elements in same order, but elements are not in same order denotes there is distortion

Time Complexity - O(nlogn)

Space Complexity - O(n)

_Optimised Approach_

Counting the inversion pair in the inorder can help us, as we can find 2 inversion pairs, and in the first inversion pair choose the greater element and in the second inversion pair choose the smaller element. But if the elements sharing an edge are swapped then we would be only able to find 1 inversion pair. What to do in that case? 
In that case both the elements of the single inversion pair will be our answer because those are the only one which are swapped.

Time Complexity - O(n)

Space Complexity - O(n)

**Q6- Build BST from unsorted array**
Keep on adding elements by traversing the tree. 

**Q7- Given a BST, Given the root and another pointer to another node, What is the next element in the inorder traversal after this pointer's node?**

- Case 1: What if there is a right subtree of the given node? -> Get the leftmost of the right subtree of the given node
- Case 2: What if there is no right subtree?


**Q8- Given a sorted array, construct a possible bst from that (unique bst) (try to make a balanced bst)**

```java
private Node construct(int[] in, int lo, int hi) {

		if (lo > hi) {
			return null;
		}

		// mid element will be root node
		int mid = (lo + hi) / 2;
		// make a new node
		Node nn = new Node();
		nn.data = in[mid];
		this.size++;

		nn.left = construct(in, lo, mid - 1);
		nn.right = construct(in, mid + 1, hi);

		return nn;

	}
```

**Q9- Convert a BST into min heap with a constraint that all values in left. Subtree are less than the values in right subtree**

