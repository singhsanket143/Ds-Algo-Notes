Updating an interval ( Lazy Propagation )
Sometimes problems will ask you to update an interval from l to r, instead of a single element. One solution is to update all 
the elements one by one. Complexity of this approach will be O(N) per operation since where are N elements in the array and 
updating a single element will take O(logN) time.
To avoid multiple call to update function, we can modify the update function to work on an interval.

Let's be Lazy i.e., do work only when needed. How ? When we need to update an interval, we will update a node and mark its 
child that it needs to be updated and update it when needed. For this we need an array lazy[] of the same size as that of 
segment tree. Initially all the elements of the lazy[] array will be 0 representing that there is no pending update. If there 
is non-zero element lazy[k] then this element needs to update node k in the segment tree before making any query operation.

To update an interval we will keep 3 things in mind.

 - If current segment tree node has any pending update, then first add that pending update to current node.
 - If the interval represented by current node lies completely in the interval to update, then update the current node and 
 update the lazy[] array for children nodes.
 - If the interval represented by current node overlaps with the interval to update, then update the nodes as the earlier update 
 function
 
Since we have changed the update function to postpone the update operation, we will have to change the query function also. 
The only change we need to make is to check if there is any pending update operation on that node. If there is a pending update
operation, first update the node and then work same as the earlier query function.


```cpp

void updateRange(int node, int start, int end, int l, int r, int val)
{
    if(lazy[node] != 0)
    { 
        // This node needs to be updated
        tree[node] += (end - start + 1) * lazy[node];    // Update it
        if(start != end)
        {
            lazy[node*2] += lazy[node];                  // Mark child as lazy
            lazy[node*2+1] += lazy[node];                // Mark child as lazy
        }
        lazy[node] = 0;                                  // Reset it
    }
    if(start > end or start > r or end < l)              // Current segment is not within range [l, r]
        return;
    if(start >= l and end <= r)
    {
        // Segment is fully within range
        tree[node] += (end - start + 1) * val;
        if(start != end)
        {
            // Not leaf node
            lazy[node*2] += val;
            lazy[node*2+1] += val;
        }
        return;
    }
    int mid = (start + end) / 2;
    updateRange(node*2, start, mid, l, r, val);        // Updating left child
    updateRange(node*2 + 1, mid + 1, end, l, r, val);   // Updating right child
    tree[node] = tree[node*2] + tree[node*2+1];        // Updating root with max value 
}

int queryRange(int node, int start, int end, int l, int r)
{
    if(start > end or start > r or end < l)
        return 0;         // Out of range
    if(lazy[node] != 0)
    {
        // This node needs to be updated
        tree[node] += (end - start + 1) * lazy[node];            // Update it
        if(start != end)
        {
            lazy[node*2] += lazy[node];         // Mark child as lazy
            lazy[node*2+1] += lazy[node];    // Mark child as lazy
        }
        lazy[node] = 0;                 // Reset it
    }
    if(start >= l and end <= r)             // Current segment is totally within range [l, r]
        return tree[node];
    int mid = (start + end) / 2;
    int p1 = queryRange(node*2, start, mid, l, r);         // Query left child
    int p2 = queryRange(node*2 + 1, mid + 1, end, l, r); // Query right child
    return (p1 + p2);
}

```


Q - Segment trees are extremely useful. In particular "Lazy Propagation" (i.e. see here, for example) allows one to compute sums over a range in O(lg(n)), and update ranges in O(lg(n)) as well. In this problem you will compute something much harder:

The sum of squares over a range with range updates of 2 types:

1) increment in a range

2) set all numbers the same in a range.

```cpp
#include <iostream>
#define ll long long int
using namespace std;
class Custom{
public:
	ll sqval;
	ll val;
	ll lazy;
	int type;
};


void build(int *arr, Custom **seg, int n, int low, int high, int node) {
	if(low > high) return;
	if(low == high) {
		seg[node] = new Custom();
		seg[node]->sqval = arr[low]*arr[low];
		seg[node]->val = arr[low];
		seg[node]->type = 0;
		seg[node]->lazy = 0;
		return;
	}
	seg[node] = new Custom();
	seg[node]->lazy = 0;
	seg[node]->type = 0;
	int mid = (low+high)/2;
	build(arr, seg, n, low, mid, 2*node);
	build(arr, seg, n, mid+1, high, 2*node+1);
	seg[node]->sqval = seg[2*node]->sqval + seg[2*node+1]->sqval;
	seg[node]->val = seg[2*node]->val + seg[2*node+1]->val;
}

void update(Custom **seg, int low, int high, int L, int R, int inc, int type, int node) {
	
	if(seg[node]->type != 0) {
		if(seg[node]->type == 1) {
			seg[node]->sqval += (2*seg[node]->lazy*seg[node]->val + (high-low+1)*seg[node]->lazy*seg[node]->lazy);
			seg[node]->val += (high-low+1)*seg[node]->lazy;
		} else if(seg[node]->type == 2) {
			seg[node]->sqval = (high-low+1)*seg[node]->lazy*seg[node]->lazy;
			seg[node]->val = (high-low+1)*seg[node]->lazy;
		}
		if(low!=high) {
			seg[2*node]->type = seg[node]->type;
			seg[2*node+1]->type = seg[node]->type;
			seg[2*node]->lazy = seg[node]->lazy;
			seg[2*node+1]->lazy = seg[node]->lazy;
		}
		seg[node]->lazy = 0;
		seg[node]->type = 0;
	}
	if(low > high or low > R or high < L) return;
	if(low >= L and high <= R) {
		if(type == 1) {
			seg[node]->sqval += 2*inc*seg[node]->val + (high-low+1)*inc*inc;
			seg[node]->val += (high-low+1)*inc;
		} else if(type == 2) {
			seg[node]->sqval = (high-low+1)*inc*inc;
			seg[node]->val = (high-low+1)*inc;
		}
		if(low != high) {
			seg[2*node]->type = type;
			seg[2*node+1]->type = type;
			seg[2*node]->lazy = inc;
			seg[2*node+1]->lazy = inc;
		}
		return;
	}
	int mid = (low+high)/2;
	update(seg, low, mid, L, R, inc, type, 2*node);
	update(seg, mid+1, high, L, R, inc, type, 2*node+1);
	seg[node]->sqval = seg[2*node]->sqval + seg[2*node+1]->sqval;
	seg[node]->val = seg[2*node]->val + seg[2*node+1]->val;
}

ll query(Custom **seg, int low, int high, int L, int R, int node) {
	if(low > high or low > R or high < L) return 0;
	if(seg[node]->type != 0) {
		if(seg[node]->type == 1) {
			seg[node]->sqval += 2*seg[node]->lazy*seg[node]->val + (high-low+1)*seg[node]->lazy*seg[node]->lazy;
			seg[node]->val += (high-low+1)*seg[node]->lazy;
		} else if(seg[node]->type == 2) {
			seg[node]->sqval = (high-low+1)*seg[node]->lazy*seg[node]->lazy;
			seg[node]->val = (high-low+1)*seg[node]->lazy;
		}
		if(low!=high) {
			seg[2*node]->type = seg[node]->type;
			seg[2*node+1]->type = seg[node]->type;
			seg[2*node]->lazy = seg[node]->lazy;
			seg[2*node+1]->lazy = seg[node]->lazy;
		}
		seg[node]->lazy = 0;
		seg[node]->type = 0;
	}
	if(low >= L and high <= R) {
		return seg[node]->sqval;
	}	
	int mid = (low+high)/2;
	ll left = query(seg, low, mid, L, R, 2*node);
	ll right = query(seg, mid+1, high, L, R, 2*node+1);
	return left+right;
}

int main(int argc, char const *argv[])
{
	int t;
	cin>>t;
	for(int i = 0; i < t; i++) {
		int n, q;
		cin>>n>>q;
		int *arr = new int[n]();
		for(int i =0;i < n;i++) {
			cin>>arr[i];
		}
		Custom** seg = new Custom*[4*n];
		build(arr, seg, n, 0, n-1, 1);
		cout<<"Case "<<i+1<<":"<<endl;
		while(q--) {
			int type;
			cin>>type;
			if(type == 2) {
				int l, r;
				cin>>l>>r;
				cout<<query(seg, 0, n-1, l-1, r-1, 1)<<endl;
			} else if(type == 1) {
				int l, r, inc;
				cin>>l>>r>>inc;
				update(seg, 0, n-1, l-1, r-1, inc, 1, 1);
			} else {
				int l, r, inc;
				cin>>l>>r>>inc;
				update(seg, 0, n-1, l-1, r-1, inc, 2, 1);
			}
		}
	}
	return 0;
}

```

Q - LCA Query using RMQ
