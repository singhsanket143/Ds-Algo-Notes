## Queue

- Linear Data Structure
- First In first Out

### Operations:

(Mention overflow and underflow conditions)
- Enqueue()
- Dequeue()

### Applications

- CPU Scheduling
- Disk Scheduling
- In real life scenario, Call Center phone systems uses Queues to hold people calling them in an order, until a service representative is free.

### Implementation

- Array
  Maintain two pointers: Front and end. 
  Both will point to -1 in the end.
  Enqueue -> rear, Deequeue -> rear
  Problems  
    - not being able to dynamically resize. 
    - front becomes equal to rear even when array is empty. 
- Circular Array

```java
//Initialisation
  
  front = -1;
  rear = -1;
  
// Enqueue

  


```
  
- LinkedList

- Stack ( 2 ways of implementation )

- Implementation of Circular Queue

### Double Ended Queue

- A very powerful data structure
- Implementation of Circular Double Ended Queue
  - Array
    - Have spacial Locality
  - LinkedList
    - Easy to resize
**Q1 - Print all binary numbers upto d digits**
Input: 3
Output: 0 1 10 11 100 101 110 111

**Q2- Given some N, and some digits 1, 2...k, find the first N numbers that can be formed from these digits. 

Note: You can do level order traversal (BFS) using queue. 


    
**Q3- Given arr[n] and window size k, find max for every window of size k. 

**Q4- Given a stream of characters and we have to find first non repeating character each time a character is inserted to the stream**
**Q5- Shortest Subarray with Sum at Least K**



 

