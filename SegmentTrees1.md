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

But here the trade-off is to answer the query of type 2 as in to update the array index we can directly access it and update it because now we have transformed it to a prefix sum array. So to handle this we need to iterate from the given index of update and iterate till the last index and maintain the prefix sum to all those index which are going to be affected by this current update.

For query of type 1 
Time Complexity - O(1)
Space Complexity - O(1)
For query of type 2
Time Complexity - O(n)
Space Complexity - O(1)

Can we optimize???

## Introduction to Segment Trees
Till now you might have encountered a lot of data structures, some of them might be linear like arrays, linked list, strings, stacks, queues etc. and some of them might were hierarchical in nature like Binary Trees, Binary Search Trees, Tries etc. 
Segment trees are one of those data structures which is basically portrayed as a hierarchical data structure but represented in a linear fashion. 

A segment tree is a binary tree build on top of an array. This structure allows aggregation queries and updates over array intervals in logarithmic time. 

Now the big question that might come to you mind is how on the earth one might think about segment trees???? It's not that obvious to think for. 

So as the name suggest, this tree divides your problem into several segments and then try to prune out those segments that are of no use for the current query and try to just use those segments which will contribute something to your answer. If there are a lot of segments present that will contribute to you answer, then their bigger aggregate segment is already maintained that can give you your answers much earlier. 

If the above arguments seems confusing to you guys then dont worry I will elaborate everything perfectly. 

Given an array A, we store the values in the leaves of a tree. At each level we combine two nodes at time and store their sum in the parent. This builds up a binary tree, as shown in the following example with an array of size 8.

arr = [2, 3, 3, 2, 6, 4, 5, 2]

                    ----27-----
                  /             \
                10               17
               /   \            /   \
             5       5       10       7
           /  \     /  \     / \     / \
          2    3   3    2   6   4   5   2


Now, suppose we update A[7] from 5 to 8. To update the tree, we start from the leaf A[7] and walk up a path of length log N to the root, updating all values on the way. In the figure below, the updated values are marked with a *.

                    ----30*----
                  /             \
                10               27*
               /   \            /   \
             5       5       10      10*
           /  \     /  \     / \     / \
          2    3   3    2   6   4   8*  2

At each node, lets see what segments are getting stored at which level
The diagram below shows that what level node is storing which corresponding segment.

                         -----30----
                       /    [1,8]    \
                     /                 \
                   10                    27
                 [1,4]                  [5,8]
               /       \              /       \
             5           5          10          10
           [1,2]       [3,4]       [5,6]       [7,8]
           /   \       /   \       /   \       /  \
          2     3     3     2     6     4     8     2
        [1,1] [2,2] [3,3] [4,4] [5,5] [6,6] [7,7] [8,8]
        
Suppose we want the sum from index 1 to 6. We start from the root and can easily observe that range [1-6] is contained in range [1-8]. If we will go left we will find [1-4] that is contained in [1-6] but not all of it. What is left is [5-6] for which we go right. Seeing [5-8], we go left and find [5-6] and stop.

What if we want sum from index 1 to 7? Again, we pick up [1-4] and go to [5-8]. We then pick up [5-6] and go right to pick up [7-7].

In general, when computing Query Type 1 where you need to calculate the answer from index X to Y, we start checking from the root node, and see if the whole range lies inside a particular node or not. If it does then the answer lies in some lower segments, otherwise we will extract answer from some left segments and some right segments. 

How do we store this tree? We can number the elements in the tree level by level, starting from the root, as we do in a heap. If there are N leaves, there are 2N-1 elements in the array, with the leaves in the last N positions. Given a position i, we can compute the positions parent(i), leftchild(i) and rightchild(i) as in a heap.
To set up the array, do something similar to constructing a heap. The array elements are stored in the last N elements. Working backwards, update A[i] as A[2i]+A[2i+1] (sum of its children).

Q- 1 -> You are given a sequence of n integers a1 , a2 , ... , an in non-decreasing order. In addition to that, you are given several queries consisting of indices i and j (1 ≤ i ≤ j ≤ n). For each query, determine the most frequent value among the integers ai , ... , aj.

https://www.spoj.com/problems/FREQUENT/

```cpp
#include<iostream>
#include <stdio.h>
#define ll long long int
using namespace std;
ll arr[100005];
class Custom {
public:
	ll leftmost_el;
	ll leftmost_val;
	ll rightmost_el;
	ll rightmost_val;
	ll ans;
	Custom(ll leftmost_el, ll leftmost_val, ll rightmost_el, ll rightmost_val, ll ans = 1) {
		this->leftmost_el = leftmost_el;
		this->leftmost_val = leftmost_val;
		this->rightmost_el = rightmost_el;
		this->rightmost_val = rightmost_val;
		this->ans = ans;	
	}
};

Custom* merge(Custom* x, Custom *y) {
		Custom* res = new Custom(0,0,0,0,0);
		res->leftmost_el = x->leftmost_el;
		res->leftmost_val = x->leftmost_val;
		res->rightmost_el = y->rightmost_el;
		res->rightmost_val = y->rightmost_val;
		res->ans = max(x->ans, y->ans);
		if(x->leftmost_el == y->leftmost_el) {
			res->leftmost_val+=y->leftmost_val;
		}
		if(x->rightmost_el == y->rightmost_el) {
			res->rightmost_val+=x->rightmost_val;
		}
		if(x->rightmost_el == y->leftmost_el) {
			res->ans = max(res->ans, x->rightmost_val+y->leftmost_val);
		}
		return res;
	}

void buildTree(ll *arr, Custom **seg, ll L, ll R, ll treeIndex) {
	if(L > R) return;
	if(L == R) {
		seg[treeIndex] = new Custom(arr[L], 1, arr[L], 1, 1);
		return;
	}
	ll mid = (L+R)/2;
	buildTree(arr, seg, L, mid, 2*treeIndex+1);
	buildTree(arr, seg, mid + 1, R, 2*treeIndex+2);
	seg[treeIndex] = merge(seg[2*treeIndex+1], seg[2*treeIndex+2]);
}

Custom* query(Custom **seg, ll L, ll R, ll S, ll E, ll treeIndex) {
	if(S > E or S > R or E < L) {
		return new Custom(0,0,0,0,0);
	} 
	if(S >= L and E <= R) {
		return seg[treeIndex];
	}
	ll mid = (S+E)/2;
	Custom* left = query(seg, L, R, S, mid, 2*treeIndex+1);
	Custom* right = query(seg, L, R, mid+1, E, 2*treeIndex+2);
	Custom* ans = merge(left, right);
	return ans;
}

int main(int argc, char const *argv[])
{
	ll n, q;
	scanf("%lld", &n);
	while(n) {
		scanf("%lld", &q);
		for(int i = 0; i < n; i++) {
			cin>>arr[i];
		}
		Custom **seg = new Custom*[4*n];
		buildTree(arr, seg, 0, n-1, 0);
		while(q--) {
			ll L, R;
			scanf("%lld%lld", &L, &R);
			Custom *result = query(seg, L-1, R-1, 0, n-1, 0);
			printf("%lld\n",result->ans);
		}
		scanf("%lld", &n);
	}
	return 0;
}

```

