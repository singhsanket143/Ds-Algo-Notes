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

```cpp
void insertionSort(int arr[], int n)  
{  
    int i, key, j;  
    for (i = 1; i < n; i++) 
    {  
        key = arr[i];  
        j = i - 1;  
  
        /* Move elements of arr[0..i-1], that are  
        greater than key, to one position ahead  
        of their current position */
        while (j >= 0 && arr[j] > key) 
        {  
            arr[j + 1] = arr[j];  
            j = j - 1;  
        }  
        arr[j + 1] = key;  
    }  
}  
  
```

# Selection Sort
This minimizes the number of swaps - O(n)
Comparisons are - O(n * n)
Not stable by default

```cpp
void selectionSort(int arr[], int n)  
{  
    int i, j, min_idx;  
  
    // One by one move boundary of unsorted subarray  
    for (i = 0; i < n-1; i++)  
    {  
        // Find the minimum element in unsorted array  
        min_idx = i;  
        for (j = i+1; j < n; j++)  
        if (arr[j] < arr[min_idx])  
            min_idx = j;  
  
        // Swap the found minimum element with the first element  
        swap(&arr[min_idx], &arr[i]);  
    }  
}  
```

**Make it Stable**

Basically in selection sort, swap that occurs at the end of each "round" can change the relative order of items having the same value.

for example, suppose you sorted 4 2 3 4 1 with selection sort.

the first "round" will go through each element looking for the minimum element. it will find that 1 is the minimum element. then it will swap the 1 into the first spot. this will cause the 4 in the first spot to go into the last spot: 1 2 3 4 4

now the relative order of the 4's has changed. the "first" 4 in the original list has been moved to a spot after the other 4.

remember the definition of stable is that

the relative order of elements with the same value is maintained.

Well, selection sort works by finding the 'least' value in a set of values, then swap it with the first value:

Code:

2, 3, 1, 1 # scan 0 to n and find 'least' value

1, 3, 2, 1 # swap 'least' with element 0.

1, 3, 2, 1 # scan 1 to n and find 'least' value

1, 1, 2, 3 # swap 'least' with element 1.

...and so on until it is sorted.

To make this stable, instead of swaping values, insert the 'least' value instead:

Code:

2, 3, 1, 1 # scan 0 to n and find 'least' value

1, 2, 3, 1 # insert 'least' at pos 0, pushing other elements back.

1, 3, 2, 1 # scan 1 to n and find 'least' value

1, 1, 2, 3 # insert 'least' at pos 1, pushing other elements back.

...and so on until it is sorted.

It shouldn't be too hard to modify an unstable selection sort algorithm to become stable.

# Bubble Sort

Stable
```cpp
void bubbleSort(int arr[], int n) 
{ 
   int i, j; 
   bool swapped; 
   for (i = 0; i < n-1; i++) 
   { 
     swapped = false; 
     for (j = 0; j < n-i-1; j++) 
     { 
        if (arr[j] > arr[j+1]) 
        { 
           swap(&arr[j], &arr[j+1]); 
           swapped = true; 
        } 
     } 
  
     // IF no two elements were swapped by inner loop, then break 
     if (swapped == false) 
        break; 
   } 
} 
```

# Counting sort

```cpp
void countSort(vector <int>& arr) 
{ 
    int max = *max_element(arr.begin(), arr.end()); 
    int min = *min_element(arr.begin(), arr.end()); 
    int range = max - min + 1; 
      
    vector<int> count(range), output(arr.size()); 
    for(int i = 0; i < arr.size(); i++) 
        count[arr[i]-min]++; 
          
    for(int i = 1; i < count.size(); i++) 
           count[i] += count[i-1]; 
    
    for(int i = arr.size()-1; i >= 0; i--) 
    {  
         output[ count[arr[i]-min] -1 ] = arr[i];  
              count[arr[i]-min]--;  
    } 
      
    for(int i=0; i < arr.size(); i++) 
            arr[i] = output[i]; 
} 
```

## Q - Analyze Bubble-3 sort
It won't actually sort the array. Ex - [5, 1], [4,1,3]
It will sort all odd index individually and even separately

