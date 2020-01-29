**Q1. Given an array of n elements, where each element is at most k away from its target position. Sort the array.**

Ex: Array: 10, 9 , 8 , 7, 4, 70, 60, 50 and k=4 
Intuition
Since each element is at most k away from its target position, the minimum of the array can be found inside the first k+1 elements.
In other words, the minimum of first window of k+1 elements will be the minimum of the array. The minimum of the next window of k+1 elements will be the second minimum of the array. And so on. 
Algo
1) Create a min heap of size k+1 using the first k+1 elements of the array. (in O(k) time)
2) One by one remove min element from heap, put it in the array, and add a new element to heap from remaining elements. (in O((n-k) logk) time.)

**Q2. Heap Sort**

Intuition
If we cunstruct a min-heap of all the elements and one by one remove the minimum from the heap, the array will be sorted. But we will be needing result array to store the sorted array.
Can we do it without using the extra space? 
Recall how we delete the root from heap. Root is sent to the last position.
We want to take the largest to the last. 
Algo
1) Build a max heap from the input data.
2) At this point, the largest item is stored at the root of the heap. Replace it with the last item of the heap followed by reducing the size of heap by 1. Finally, heapify the root of tree.
3) Repeat step 2 till the size is 1.

**Q3. Given an unsorted array return the k largest numbers from the array.**
Ex: 1, 23, 12, 9, 50, 2, 30 and k=3 
ans: 23,50,30 
Intuition
Select k elements from the array in such a way that the minimum of those k elements is the kth largest element of the array. 
Algo
1) Build a Min Heap using first k elements of the given array. (in O(k) time). We want to have k largest elements inside this heap.
2) For each element, after the kth element, compare it with root of the heap. If the element is greated than the root, make it the root and call heapify else ignore.(in O((n-k)Logk) time.)
3) After step 2, elements in the min heap will be the k largest elements of the array.

**Q4. Given an unsorted array. Find the maximum difference between two subsets of m elements.**

Ex: Array: 1, 3, 2, 5, 4 
Ans: 4 [(3+2+4+5) - (1+3+2+4)] 
Intuition
To maximize the difference select subsets of m largest elements and m smallest elements. 
Algo
How to find m largest/smallest elements from an array without sorting?
See previous problem.

**Q5. Given that integers are read from a data stream. Come up with an online algorithm for finding the median of elements read so far in efficient way.**
Ex: After reading 1st element of stream - 5 -> median - 5
After reading 2nd element of stream - 5, 15 -> median - 10
After reading 3rd element of stream - 5, 15, 1 -> median - 5
After reading 4th element of stream - 5, 15, 1, 3 -> median - 4, so on...
Intuition
If we are able to maintain a partition in the array in such a way that the first n/2 elements (n/2 small elements) are on one side(say left part) and next n/2 elements(n/2 large elements are on the other side, say right part) then the maximum of the left part and the minimum of the right part are the only number which are required to get the median. 

-> How to decide whether a newelement goes to the right or the left side? 
If new element is smaller than the median, it goes to the left side else to the right side.

-> How to get the min and max efficiently? 
Keep elements of left part in max-heap and elements of right part in min heap.

-> How to keep the size of the two part equal? 
If diff in size becomes greater than one, then pop the root of the larger heap (larger in size) and push in the smaller one.


**Q6. Find Kth smallest element in a row-wise and column-wise sorted 2D array**

Intuition
1) The first element (a[0][0]) will always be the 1st minimum.
2) Now, who all are the contenders of the second minimum? 
a[0][1] & a[1][0]. No elements other than these two can be the second minimum (Why?).
3) If we know that (A[i][j]) is the kth minimum then (A[i+1][j]) and (A[i][j+1]) will come up as the contenders of the next minimum.
Algo:
1) Create a min heap using A(0,0).
2) Pop the top element.
3) If the poped element was A(i,j) push A(i+1,j) and A(i,j+1) in heap.(only if they are not already present)
4) Repeat from step 2, k times.
