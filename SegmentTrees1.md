Let's say you have a problem in your hand such that, You have been given an array of integers A. Apart from this you will be given Q queries
In each query you will get two numbers L, R denoting some indices of the given array. What you are supposed to do, we are supposed to tell the
sum of all the numbers lying between the range [L, R]. Apart from this sometimes you can also get a query which will contain two numbers idx, val
in which you are supposed to update the given array's `idx` index with `val` value. Both the queries can come randomly and you supposed to process
them in as efficient manner as possible.

What are the possible solutions you can think of???

### Naive Approach

For query of type 1 - You can process the array in linear fashion and just iterate from index L to R and sum up the values.
Time Complexity - O(n)
Space Complexity - O(1)
For query of type 2 - You can just update the index of the array in const time as arrays allows that operation easily.
Time Complexity - O(1)
Space Complexity - O(1)

The problem in above approach is type 1 query is taking time complexity O(n)

Can we optimize???

### Approach 2

Let's say F(x, y) is a function which calculates sum of all elements from index X to index Y, then we can say that
F(x, y) = F(1, x-1) - F(1, y)
We can observe F(1, y) is the prefix sum of elements till index y and same for F(1, x-1)

So if we can update the given array as a prefix sum array

Then we can answer the query of type 1, in O(1) time 

But here the trade-off is to answer the query of type 2 as in to update the array index we can directly access it and update it because now we have transformed it to a prefix sum array. So to handle this we need to iterate from the given index



