## Intro

Let's talk about another sorting algorthim today - Insertion Sort.

Insertion Sort is not the best sorting algorithm, in terms of performance, but it is a pretty intuitive sorting technique.

Let's see how. 

## Logic

Let's take the example of cards.  
Let's say we have a set of cards in our right hand (9, 3, 6, 4) and we want to arrange them in the increasing order.  

Our left hand is initially empty. At all times, we will make sure that the cards in our left hand remain in sorted order.

We now take each card one by one,  
from our right hand,
and insert the card,
in the correct position,
in our hand hand.

1. The first card is 9. There is no other card in the leftt hand, so 9 simply goes to the left hand. 

2. The next card is 3. When we take 3 to the left hand, we place it before 9 to make sure that the cards are sorted. 

3. At any stage during the process, the right hand is going to be unsorted, and the left hand is going to be sorted. 

4. The next card is 6. We insert it between 3 and 9 in the left hand. 

5. The last card is 4 and it goes between 3 and 6 in the left hand. 

FINALLY, we have a sorted arrangement in the left hand.

Basic idea is that we have divided the cards into two parts i.e., sorted part and unsorted part. Initially, all the cards are in the unsorted part and the sorted part is empty. 
At a time, we are picking up one card from the unsorted part and INSERTING it in its right position in the sorted part. 

We are done when the unsorted part is empty. 


We can follow the similar structure for array as well. 

## Dry Run

Let's say we want to sort an array of Integers in Sorted Order. 
25, 17, 31, 13, 12.
1. Divide the array into two parts - Sorted and Unsorted.

2. Intially the first element of the array, 25 is part of the sorted part and rest all the elements are in the unsorted part. (Why only one element in sorted part? Because a single element is always going to be sorted)

3. Now we go on to pick the elements from the unsorted subset and insert them at their right position in the sorted subset. So, we are basically expanding the sorted part and till unsorted subset becomes empty. 
In the first iteration, we pick 17 and create a hole at its position. Now to insert 2 at its right position in the sorted part, we shift all elements greater than two to the right. Now we are sorted till index 1. 

..........

## PseudoCode

```java
void sort(int[] arr) {
    int n = arr.length;
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j = j - 1;
        }
        arr[j+1] = key;
    }
}
```


## Time Complexity

Now let's try to analyse the time complexity of this algorithm. 
1. In the worst case, the array given to us can be in decreasing order and we will be asked to arranged it in increasing order. 
For 5, 4, 3, 2, 1 both the nested loops in the pseudocode will run their maximum iteration and the time complexity in that case will be O(n^2). ( Dry Run required again???) 

2. Now let's the consider the time complexity in best case. The best case will happen when the elements given to us in the array are already sorted. When we already have the sorted array, we will never go into the second while loop ever because the second condition of while loop will never hold true and the outer loop will execute (n-1 times) giving us the time complexity of O(n)


## When exactly to use insertion sort (Not present on website)

The insertion sort algorithm comes handy when you want to sort a *almost sorted array*. 

For eg: Consider the array with elements 4 7 3 8 9.

Here we can see that except the element 3, all the other elements are at their right position. At this point, you can use Insertion Sort because with this algorithm, you will have to do minimum amount of swaps and the sorted array very fast. 
