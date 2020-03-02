## What do u mean by sorting?
It is a process of permuting in a particular order.

### What's the bruteforce approach?
Calculate all possible factorials in O(n*n!) time

## What we look for when we deal with sorting?
 - We care about time and space - Best/Avg/Worst
 - We care about number of comparison
 - No of swaps
 - Stability will be one factor
 - If the sort is Inplace or not
 
 
Let me make an argument
**O(time) >= O(allocation_of_space + no_of_comparison + no_of_swaps)**

Why is this true?

Let's say you have a ship of container and you have to sort them, then comparison is not as expensive as swapping because u need labour to do so
that's why taking care of swaps is also relevant for us

## What is stability?
The relative order of elements should be maintained
If two objects are equal according to some key/function they must retain their original relative order

## Use of Stability
In excel and in sorting files

# Insertion Sort
Invariant of insertion sort - In the ith iteration i-1 elemenets are sorted
No of swaps in avg and worst - O(n * n)
Best no of swaps - O(1)

Best Time - O(n)
Worst Time - O(n * n)
Avg Time - O(n * n)

Discuss Binary search Optimisation

It Can be stable if comparison is not >= .

If array is almost sorted Insertion sort is going to be good

# Selection Sort
This minimizes the number of swaps - O(n)
Comparisons are - O(n * n)


## Q - Analyze Bubble-3 sort
It won't actually sort the array. Ex - [5, 1], [4,1,3]
It will sort all odd index individually and even separately

