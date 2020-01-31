## Intro

Today we are going to talk about another sorting algorthim i.e., Insertion Sort. Insertion Sort is not the best sorting algorithm in terms of performance but it is a little bit more efficient than Bubble Sort and Selection Sort. It is also a pretty intuitive sorting technique. Let's see how. 

## Logic

To explain the logic of Insertion Sort, let's take the example of cards. Let's say we have a set of cards in our hand (9, 6, 3, 4) and we want to arrange them in the increasing order. There are many ways to do that but one of the most intuitive ways is to keep all the cards intially in the left hand. Then, start taking cards one by one from the left hand and try to build a sorted arrangement in the right hand. 

1. Since the first card is 9, and there is no other card in the right hand, so 9 simply goes to the right hand. 

2. Now we take the next card from the left hand i.e., 3. When you take 3 to the right hand, you place it before 9 to make sure that the cards are sorted. 

3. At any stage during the process, the left hand is going to be unsorted, and the right hand is going to be sorted. 

4. Now we pick next card, 6, from the left hand and insert it between 3 and 9 in the right hand. 

5. The last card in the left hand is 4 and it needs to be placed between 3 and 6 in the right hand. 

FINALLY, we have a sorted arrangement in the right hand. 

Basic idea is that we have divided the cards into two parts i.e., sorted part and unsorted part. Initially, all the cards are in the unsorted part and the sorted part is empty. 
At a time, we are picking up one card from the unsorted part and INSERTING it in its right position in the sorted part. 

Let's try a boundary line, and try to visualise it. ELements to the left of this boundary are sorted and elements to the right of this boundary are unsorted.

Initially all the cards in the unsorted part. Now, we pick each card at a time and INSERT it into the sorted part. 
Since, it is the first card, we simply put it into the sorted part. Then we pick the next card 3 and insert 

.....

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
void sort(int arr[])
    {
        int n = arr.length;
        for (int i=1; i<n; ++i)
        {
            int key = arr[i];
            int j = i-1;
            
            while (j>=0 && arr[j] > key)
            {
                arr[j+1] = arr[j];
                j = j-1;
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
