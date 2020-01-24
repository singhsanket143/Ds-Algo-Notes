### Heaps

Problem: 
Given n ropes, let's say of length of each rope is 4, 3, 2 and 6. Now you have to join all these ropes and form a rope of single length with a constraint that you can only join two ropes at a time. Also, each join operation, has a cost associated with it i.e., C = L1 + L2

**Solution** : Taking the minimum ropes first, 3 + 2 = 5, 5 + 4 = 9, 9 + 6 = 15 i.e., total cost = 29. 
Will taking the cost of minimum length ropes first, always work?

#### Binary Heap 
- Binary Tree
- Complete Binary Tree
- All the elements of the heap should follow either min/max property
- Root and children value can be same
- Maximum/Minimum value will be present at the root node


Given the left substree is a maxheap and the right subtree is also a max heap. What can be done to make the entire tree a max heap?
- only swapping the values is allowed
- Select the bigger child and swap
- Time complexity of the process - O(log n)

**How to build a heap?**

5, 2, 10, 1, 7 , 8

Build a max heap.

What data structure to use? Array or Trees?
- If you use a Tree, each node is storing three things - Node value, left child and right child. 
- In case of array, binary tree is memory efficient, cache efficient and no null node is between when storing the values.
- The root node will be at index 0. Left child will be present at Index - 2*i + 1. Right child will be present at index 2*i + 2. 


