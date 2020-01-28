
### Questions on Heaps

**Q- Given an unsorted array, with a special property that it is not completely unsorted. It is a K-sorted array meaning that 
every element in the array is at a distance atmost K from its sorted position.**
  
  **Eg: 10, 9, 8, 7, 4, 70, 60, 50      Here k = 4**
  
  **Sorted position: 4, 7, 8, 9, 10, 50, 60, 70**
  
  **Here every element is at a distance atmost K from its sorted position.**
  
  **Your job is to sort the array**
  
    _Observation_: 1. For the element at index 0, its correct position will always be in the window of size k + 1.

    2. First element of the sorted array, will be the minimum element in the window of size k + 1. Similarly, we can make the observation for secod element of the sorted array as well.

    Job is to find the minimum element in the sliding window approach. 

    Algorithm:

    1. Find the minimum of every window and slide the window by one step.
    2. Which data structure can help in finding the minimum in an efficient manner? Min Heap.

    Time Complexity: O(nlogK) + O(K)

**Q- Given a completely unsorted array, can you sort them using heap**

    Eg: 4, 10, 5, 3, 1

    Approach 1: Put all the elements in the min-heap. Extract the minimum elements one by one. 

    Time Complexity: O(nlogn) + O(n)
    Space Complexity: O(n)

    Approach 2: Make a In place Min heap. Remove elements one by one from the min heap. But the output will be in descending order. You need to reverse it in order to get ascending order.

    Space Complexity: O(1)
    Time Complexity: O(nlogn) + O(n)

    Approach 3: To avoid the extra reversl instead of a min heap make a max heap

    Space Complexity: O(1)
    Time Complexity: O(nlogn) + O(n)

    - Heap sort has more swaps than quick that's why avoided in internal sorting algorithm
  
  
**Q- Given a row wise and column wise sorted array. Find the Kth smallest element**

    10, 20, 30, 40
    15, 25, 35, 45
    24, 29, 37, 48
    32, 33, 39, 50


      Similar to merge K sorted arrays. Make a heap of size K using all the first index elements from each row. Then just pop min element and insert the next possible element. After K deletions u will have the answer.

      Time Complexity: O(no_of_rows) + O(klog(no_of_rows))

      But do we need to make a heap of size no_of_rows ?

      No

      Why? Because as the columns and rows are sorted. Each element at (i, j) gives you two more contenders (i+1, j) and (i, j+1).

      Time Complexity - O(k) + Oklogk)
  
  
  
**Q- Running median in stream of integers**

    Brute Force: Insertion Sort
    Optimised Approach : Maintain 2 heaps one max and one min heap.
    


**Q- Given an unsorted array, a number K and a number X, such that you need to find K closest element To X in the array

    Ex - -10, -50, 20, 17, 80
    K = 2
    X = 20
    Ans = 20, 17

    Prepare a max heap of (element, x - element) of Size K and in each iteration compare the new element, If the diff is lesser than the diff in the top of heap, then pop element from heap and insert the new element with thte corresponding difference.

    Time Complexity - O(k) + O((n-k)logK)
  
  
