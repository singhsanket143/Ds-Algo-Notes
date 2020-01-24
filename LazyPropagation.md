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
