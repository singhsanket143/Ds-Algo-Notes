**Binary Search Tree**
- Extension of Binary Tree
- All nodes in left subtree will be smaller than root.
- All nodes in right subtree will be greater than root.
- Inorder traversal yields sorted ordering of the element

**How to handle equal elements?**

- Either keep a count on every node
- Same elements can either go in left or right subtree

**Q1- Build BST from unsorted array**
Keep on adding elements by traversing the tree

**Q2- Given a BST, somebody swapped 2 elements, Find out which pair was swapped?**

**Trivial Approach**

- Take inorder of the given tree
- Copy the inorder in a different array and sort it 
- The indexes with different values gives us sorted elements

Intuition - Had it been a perfect bst, both the array would be having same elements in same order, but elements are not in same order denotes there is distortion

Time Complexity - O(nlogn)
Space Complexity - O(n)

**Optimised Approach**

Counting the inversion pair in the inorder can help us, as we can find 2 inversion pairs, and in the first inversion pair choose the greater element and in the second inversion pair choose the smaller element. But if the elements sharing an edge are swapped then we would be only able to find 1 inversion pair. What to do in that case? 
In that case both the elements of the single inversion pair will be our answer because those are the only one which are swapped.

Time Complexity - O(nlogn)
Space Complexity - O(n)




**Q7- Given a sorted array, construct a possible bst from that (unique bst) (try to make a balanced bst)**

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
**Q7- Check if a given BT is BST**
Approach1: Write inorder traversal
Approach2: 3 conditions:
- left subtree is a BST
- right subtree is a BST
- root is greater than the max value in left subtree
- root is less than the lowest value in right subtree
**Q7- Print in Range**

**Q7- Largest Binary Search Tree in BT**

**Q7- Valid Binary Search Tree**

