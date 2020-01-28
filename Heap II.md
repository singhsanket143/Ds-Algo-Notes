
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
  
  Approach 2: Make a Max heap. Remove elements one by one from the max heap. 
