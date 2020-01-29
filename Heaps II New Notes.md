**Q1. Given an array of n elements, where each element is at most k away from its target position. Sort the array.**

Ex: Array: 10, 9 , 8 , 7, 4, 70, 60, 50 and k=4 

_Brute Force Approach_: Insertion Sort 

  The inner loop will run at most k times. To move every element to its correct place, at most k elements need to be moved.  So overall complexity will be O(nk)
  
_Intuition_

Since each element is at most k away from its target position, the minimum of the array can be found inside the first k+1 elements.
In other words, the minimum of first window of k+1 elements will be the minimum of the array. The minimum of the next window of k+1 elements will be the second minimum of the array. And so on. 

_Algo_

1) Create a min heap of size k+1 using the first k+1 elements of the array. (in O(k) time)

2) One by one remove min element from heap, put it in the array, and add a new element to heap from remaining elements. (in O((n-k) logk) time.)


```
private static void kSort(int[] arr, int n, int k)  
    { 
  
        // min heap 
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(); 
  
        // add first k + 1 items to the min heap 
        for(int i = 0; i < k + 1; i++) 
        { 
            priorityQueue.add(arr[i]); 
        } 
  
        int index = 0; 
        for(int i = k + 1; i < n; i++)  
        { 
            arr[index++] = priorityQueue.peek(); 
            priorityQueue.poll(); 
            priorityQueue.add(arr[i]); 
        } 
  
        Iterator<Integer> itr = priorityQueue.iterator(); 
  
        while(itr.hasNext())  
        { 
            arr[index++] = priorityQueue.peek(); 
            priorityQueue.poll(); 
        } 
  
    } 
```

Time Complexity:O(k) + O((n-k) logk)

Space Complexity: O(k)

**Q2. Heap Sort**

Eg: 4, 10, 3, 5, 1

_Intuition_

1. If we cunstruct a min-heap of all the elements and one by one remove the minimum from the heap, the array will be sorted. But we will be needing result array to store the sorted array.

2. Can we do it without using the extra space? 

Recall how we delete the root from heap. Root is sent to the last position.
We want to take the largest to the last. 

_Algo_

1) Build a max heap from the input data.

2) At this point, the largest item is stored at the root of the heap. Replace it with the last item of the heap followed by reducing the size of heap by 1. Finally, heapify the root of tree.

3) Repeat step 2 till the size is 1.

Time complexity: O(nLogn).

Time complexity: O(1).

**Q3. Given an unsorted array return the k largest numbers from the array.**

Ex: 1, 23, 12, 9, 50, 2, 30 and k=3 

Ans: 23,50,30 

_Intuition_

Select k elements from the array in such a way that the minimum of those k elements is the kth largest element of the array. 
Algo
1) Build a Min Heap using first k elements of the given array. (in O(k) time). We want to have k largest elements inside this heap.

2) For each element, after the kth element, compare it with root of the heap. If the element is greated than the root, make it the root and call heapify else ignore.(in O((n-k)Logk) time.)

3) After step 2, elements in the min heap will be the k largest elements of the array.

Time Complexity: O(k) + O((n-k)logk)

Space Complexity: O(k)

**Q4. Given an unsorted array. Find the maximum difference between two subsets of m elements.**

Ex: Array: 1, 3, 2, 5, 4 

Here m = 4;

Ans: 4 [(3+2+4+5) - (1+3+2+4)] 

_Intuition_

To maximize the difference select subsets of m largest elements and m smallest elements. 

_Algo_

How to find m largest/smallest elements from an array without sorting? Use Max-Heap and Min-Heap.

Time Complexity: O(m) + O((n-m)logm)

Space Complexity: O(m)

**Q5. Given that integers are read from a data stream. Come up with an online algorithm for finding the median of elements read so far in efficient way.**
Ex: After reading 1st element of stream - 5 -> median - 5

After reading 2nd element of stream - 5, 15 -> median - 10

After reading 3rd element of stream - 5, 15, 1 -> median - 5

After reading 4th element of stream - 5, 15, 1, 3 -> median - 4, so on...

_Brute Force Approach_ : Using Insertion Sort. 

Time Complexity: O(n2)

_Intuition_

Is it always necessary to have the array in the sorted form? I just need the middle element at its right position. 

Here, 4, 3, 5, 2, --10--, 20, 25, 17, 12.

Here only correct position of 10 matters. Order of elements before and after it does not matter. 

If we are able to maintain a partition in the array in such a way that the first n/2 elements (n/2 small elements) are on one side(say left part) and next n/2 elements(n/2 large elements are on the other side, say right part) then the maximum of the left part and the minimum of the right part are the only number which are required to get the median. 

-> How to decide whether a newelement goes to the right or the left side? 

If new element is smaller than the median, it goes to the left side else to the right side.

-> How to get the min and max efficiently? 

Keep elements of left part in max-heap and elements of right part in min heap.

-> How to keep the size of the two part equal? 

If diff in size becomes greater than one, then pop the root of the larger heap (larger in size) and push in the smaller one.



Time Complexity: O(nlogn)

**Q6. Find Kth smallest element in a row-wise and column-wise sorted 2D array**

 10, 20, 30, 40
 15, 25, 35, 45
 24, 29, 37, 48
 32, 33, 39, 50
 
_Intuition_

1) The first element (a[0][0]) will always be the 1st minimum.
2) Now, who all are the contenders of the second minimum? 
a[0][1] & a[1][0]. No elements other than these two can be the second minimum (Why?).
3) If we know that (A[i][j]) is the kth minimum then (A[i+1][j]) and (A[i][j+1]) will come up as the contenders of the next minimum.

_Algo:_

1) Create a min heap using A(0,0).
2) Pop the top element.
3) If the poped element was A(i,j) push A(i+1,j) and A(i,j+1) in heap.(only if they are not already present)
4) Repeat from step 2, k times.

Time Complexity: O(k) + O(klogk)

Space Complexity: O(k)
**Q7- Given an unsorted array, a number K and a number X, such that you need to find K closest element To X in the array**

  Ex - -10, -50, 20, 17, 80
  
  K = 2
    
   X = 20
    
    Ans = 20, 17

  Prepare a max heap of (element, x - element) of Size K and in each iteration compare the new element, If the diff is lesser than the diff in the top of heap, then pop element from heap and insert the new element with thte corresponding difference.


Time Complexity: O(k) + O((n-k)logK)
  

**Q8- K-th Smallest Prime Fraction**

A sorted list A contains 1, plus some number of primes.  Then, for every p < q in the list, we consider the fraction p/q.
What is the K-th smallest fraction considered?  Return your answer as an array of ints, where answer[0] = p and answer[1] = q.

```
Examples:

Input: A = [1, 2, 3, 5], K = 3

Output: [2, 5]

Explanation:

The fractions to be considered in sorted order are:

1/5, 1/3, 2/5, 1/2, 3/5, 2/3.

The third fraction is 2/5.

Input: A = [1, 7], K = 1

Output: [1, 7]
```

Time Complexity: Time Complexity: O(k) + O((K)logK)

Space Complexity: O(k)

**Q9- Huffman Encoding** (Optional)


### Homework Problem

**Q9- Rainwater Trapping Problem 3-D**

https://leetcode.com/problems/trapping-rain-water-ii/
