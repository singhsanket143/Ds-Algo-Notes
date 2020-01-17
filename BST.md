**Binary Search Tree**
- Extension of Binary Tree
- All nodes in left subtree will be smaller than root.
- All nodes in right subtree will be greater than root.

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

