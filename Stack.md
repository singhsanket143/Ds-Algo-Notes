
## Stack

- Visualisation by a stack of plates. 

- Single Ended Structure. 
- Abstract Datatype 

The definition of ADT only mentions what operations are to be performed but not how these operations will be implemented. It does not specify how data will be organized in memory and what algorithms will be used for implementing the operations. It is called “abstract” because it gives an implementation-independent view. The process of providing only the essentials and hiding the details is known as abstraction.

- Linear data structure 

A linear data structure traverses the data elements sequentially, in which only one data element can directly be reached.

- LIFO (Last In First Out)

### Stack Operations

- Push (Adds an item in the stack) 
- Pop (Removes an item from the stack)

### Implementation of Stack

- *Array* (Keep the two conditions in mind during interviews)
  
  - Stack Overflow - Adding an element to the stack which is already filled. 
  - Stack Underflow - Deleting an element from stack which is already empty. 
  
  - **Pros**: Easy to implement. Memory is saved as pointers are not involved. 
  - **Cons**: It is not dynamic. It doesn’t grow and shrink depending on needs at runtime.
  
  - Can use Vectors/ArrayList also.

- *LinkedList*

  - Push() - Add at head. O(1)
  - Pop() - Remove at Head. O(1)
  
  - **Pros:** The linked list implementation of stack can grow and shrink according to the needs at runtime.
  - **Cons:** Requires extra memory due to involvement of pointers.

- *Queue* - Will discuss later


### Application of Stack

- Recursion
- Undo/Redo feature at many places like editors, photoshops. 
- Forward and backward feature in web browser. 
- Arithmetic Expression Evaluation
  
  Prefix  +ab
  Infix   a+b
  Postfix ab+
  
- Using factorial example, explain callstack.

*Iterative code better than recursion because you might run out of memory space* 

**Q1- Valid Paranthesis** (1st Question)

Input: "()[]{}"
Output: true

Approach: 

https://leetcode.com/problems/valid-parentheses/solution/

```java
public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();
        for(int i = 0 ; i < s.length(); i++) {
            char ch = s.charAt(i);
            if(ch == '(' || ch == '[' || ch == '{') {
                st.push(ch);
            } else {
                if(st.isEmpty()) return false;
                char p = st.peek();
                if(ch == ')' && p != '(') return false;
                else if(ch == ']' && p != '[') return false;
                else if(ch == '}' && p != '{') return false;
                else st.pop();
            }
        }
        return st.isEmpty();
    }

```

Time Complexity: O(n)
Space Complexity: O(n)

**Q2- Remove consecutive duplicates in a string**               
                                                                                                                           
String: kabbal 
Output: kl

*Special case*

String: aaa 
Output: a

Time Complexity: O(string.length)
Space Complexity: O(string.length)



**Q4- Stock Span Problem** 

**The span Si of the stock’s price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than or equal to its price on the given day.**

For example, 

If an array of 7 days prices is given as {100, 80, 60, 70, 60, 75, 85}, then the span values for corresponding 7 days are {1, 1, 1, 2, 1, 4, 6}

**Approach 1** -> Naive Approach

Traverse the input price array. For every element being visited, traverse elements on left of it and increment the span value of it while elements on the left side are smaller.

*Time Complexity:* O(n^2)

*Space Complexity:* O(1)

**Approach 2** -> Optimised Approach

- If arr[i] < arr[i - 1], then the span of arr[i] = 1.

- If value at arr[i] > arr[i-1], then all the elements in the span of arr[i - 1] will be included in my span, so it makes no sense to make those calculations again. We can simply jump back to that element which was not a part of span of arr[i-1]. 


```java
public static int[] StockSpan(int[] prices) throws Exception {

		Stack stack = new Stack(prices.length);
		int[] span = new int[prices.length]; // resultant array

		stack.push(0); // put index of first stock to the stack
		span[0] = 1; // update span

		for (int i = 1; i < prices.length; i++) {

			while (!stack.isempty() && prices[i] > prices[stack.top()]) {

				stack.pop();
			}

			if (stack.isempty()) {

				span[i] = i + 1; // all stocks removed
			} else {

				span[i] = i - stack.top();
			}
			stack.push(i);
		}
		return span;

	}
```
Time Complexity: O(n)

Space Complexity: O(n)

**Q2- Next Greater Element I**
Find the just greater element on right side of each element.
Ex - 4 5 2 25
Ans- 5 25 25 -1

Ex - 10 7 4 2 9 10 11 3 2
Ans- 11 9 9 9 10 11 -1 -1 -1

_Approach 1:_ Use two loops: The outer loop picks all the elements one by one. The inner loop looks for the first greater element for the element picked by the outer loop. If a greater element is found then that element is printed as next element, otherwise -1 is printed.

Time Complexity: O(n^2)
Space Complexity: O(1)

_Approach 2:_
  Intuition:
  In case of a decreasing sequence, the answer is always going to be -1 for all elements till I dont encounter a increasing   sequence/number. 
  ```
  For eg: 5 4 3 2 1        
	  
	  -1 -1 -1 -1 -1
          
          5 4 3 2 1 10
          10 10 10 10 10 -1
          
          For all the elements less than 10 in a decreasing sequence are going to have the answer 10. 
          
          11 4 3 2 10 12
          
          Till 2, it is a decreasing sequence. After that, it is a increasing sequence then. So, for all the elements less 
	  than 10, the elements are going to have an answer 10. 
          Now the question is reduced to 11 10 12. Again 11 and 10 is a decreasing sequence, so the answer for them is going           to be 12 12. 
          
```

```java
static void printNGE(int arr[], int n)  
    { 
        int i = 0; 
        stack s = new stack(); 
        s.top = -1; 
        int element, next; 
        s.push(arr[0]); 
        for (i = 1; i < n; i++)  
        { 
            next = arr[i]; 
            if (s.isEmpty() == false)  
            {  
                element = s.pop(); 
                while (element < next)  
                { 
                    System.out.println(element + "-->" + next); 
                    if (s.isEmpty() == true) 
                        break; 
                    element = s.pop(); 
                } 
                if (element > next) 
                    s.push(element); 
            } 
            s.push(next); 
        } 
        while (s.isEmpty() == false)  
        { 
            element = s.pop(); 
            next = -1; 
            System.out.println(element + "-->" + next); 
        } 
```
Time Complexity: O(n) 
Space Complexity: O(n)

**Q5- Next Greater Element II**
Consider the case of circular array
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
```java
public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Stack < Integer > stack = new Stack < > ();
        HashMap < Integer, Integer > map = new HashMap < > ();
        int[] res = new int[findNums.length];
        for (int i = 0; i < nums.length; i++) {
            while (!stack.empty() && nums[i] > stack.peek())
                map.put(stack.pop(), nums[i]);
            stack.push(nums[i]);
        }
        while (!stack.empty())
            map.put(stack.pop(), -1);
        for (int i = 0; i < findNums.length; i++) {
            res[i] = map.get(findNums[i]);
        }
        return res;
    }
```
Time complexity : O(m+n)O(m+n)
Space complexity : O(m+n)O(m+n).

**Q6- Given only two operations i.e., push() and pop(), implement insertAtBottom() function** (3

Approach 1: Using Extra Stack

Approach 2: Using Recursion

```java

insertAtBotton(Stack s, int n){
  if(s.isEmpty()){
    s.push(n);
  }
  int temp = s.pop();
  insertAtBottom(s, n);
  s.push(temp);
}

```

Time Complexity: O(n)

Space Complexity: O(n)
 
**7- Reverse a stack**  

(Perform Reversal in same stack)

Approach 1: 

```java

reverse(Stack s){
  if(s.isEmpty()){
    return;
  }
  int temp = s.pop();
  reverse(s, n);
  insertAtBottom(s, temp);
}
```

Time Complexity:

Pushing one element at the bottom - O(n)
Pushing n elements at the bottom - O(n^2)

Space Complexity:

Approach 2: Take two auxillary stack

Time Complexity: O(n)

Space Complexity: O(n)

**Q8- Implement Sorting using stack**

The idea of the solution is to hold all values in Function Call Stack until the stack becomes empty. When the stack becomes empty, insert all held items one by one in sorted order. Here sorted order is important.

Similar to above question. Just implement insertInSortedWay(). 

```java

sortStack(stack S)
    if stack is not empty:
        temp = pop(S);  
        sortStack(S); 
        sortedInsert(S, temp);
 
 
 sortedInsert(Stack S, element)
    if stack is empty OR element > top element
        push(S, elem)
    else
        temp = pop(S)
        sortedInsert(S, element)
        push(S, temp)
 
 ```
 
Time Complexity: O(n^2)

Space Complexity: O(n) 

**Q9- Implement getMin() function**

**Approach 1:** 

https://leetcode.com/articles/min-stack/

Using another stack.  

Space Complexity: O(n)

Time Complexity: O(1)

```java
public void push(int x) {
        st.push(x);
        if(minst.isEmpty()){
           minst.push(x); 
        }else if(x <= minst.peek()){
            minst.push(x);
        }
    }
    
    public void pop() {
        int val = st.pop();
        if(val == minst.peek()){
            minst.pop();
        }
    }
```

**Approach 2:** 

Lets suppose than new element to be added is `x` and the old minimum is `min` 

Now if x < min -> then we were pushing this into our auxillary stack, But here we are supposed to save the space. So in order to save the space what can think of? 
May be we can take a varibale that can store current minimum, but the issue is if we will pop this element from the stack then we will loose access to the previous minimum

Can we do something to store the value of previous minimum ??????

If x < min, then x - min < 0 (i.e. value if x - min is negative)
Now what we can do is instead of storing x in our space we can store x - min in our stack. Why because at any point of time we can extract the old minimum from the equation . How??

2 -> 3 -> 4 -> 1

After addition of 1 my current minimum will become 1, but if we pop() the stack and remove one how will you get 2??
Instead before adding 1 the value of min was equal to 2. So instead of pushing 1, push 1 - 2 (i.e. x - min) equals to -1 in stack. 

Stack becomes 2 -> 3 -> 4 -> -1 and the new min becomes , min = 1

Now when we pop the stack we know if the element at top of stack is negative then removing this element will change the current min of stack. After popping we will update min as min = min - st.top() => min = 1 - (-1) = 2
So min will be updated to 2 and stack becomes 2 -> 3 -> 4

But wait!!!
This approach only work for stack having positive elements, what will we do if also have negative elements in the stack???? How to keep a check that when we are supposed to update the min????

if x < min => x - min < 0 then adding x on both sides

2x - min < x,

i.e if x was the new min which is supposed to be lesser than all elements of stack, and 2x - min is lesser than x also then we can say that 2x - min can be stored in the stack!!!

So whenever a new element comes which is less than our current min, store 2x - min in the stack and update min to be equal to x.
How this handles negative elements, because now we no more need to trigger the update min action on encountering the negative element. When we see that ok, top of stack is less than current min, the before popping we update min to be 
min = 2*min - st.top()

Space Complexity: O(1)
Time Complexity: O(1)




Q- https://www.hackerearth.com/practice/data-structures/stacks/basics-of-stacks/practice-problems/algorithm/monk-and-order-of-phoenix/description/

![Screenshot 2020-01-08 at 7 26 58 PM](https://user-images.githubusercontent.com/29747452/71984365-b7c1f100-324e-11ea-94c4-88c9e679f0f3.png)

![Screenshot 2020-01-08 at 7 27 14 PM](https://user-images.githubusercontent.com/29747452/71984364-b7c1f100-324e-11ea-8f09-239417073859.png)

![Screenshot 2020-01-08 at 7 39 32 PM](https://user-images.githubusercontent.com/29747452/71984363-b7295a80-324e-11ea-8fc7-4452563fef71.png)

```cpp
#include <bits/stdc++.h>
#define ll long long
using namespace std;
const int ma = 1e5;
vector < ll >  v[100];
stack <ll> st;
int n;
int bs(int i, int val)
{
	int l = 0, r = v[i].size();
	while(l<r)
	{
		int mid = (l+r)/2;
		if(v[i][mid]>val)
			r = mid;
		else 
			l = mid+1;
	}
	if(v[i][l]>val)
		return l;
	return -1;
}
bool check()
{
		ll cur = st.top();
		for(int i=1;i<n;i++)
		{
			int ans = bs(i,cur);
			if(ans==-1)
				return false;
			else
				cur = v[i][ans];
		}
		return true;
}
int main()
{
	//freopen("in00.txt","r",stdin);
	//freopen("out00.txt","w",stdout);
	int x,y,q;
	cin>>n;
	for(int i=0;i<n;i++)
	{
		cin>>x;
		for(int j=0;j<x;j++)
		{
			cin>>y;
			v[i].push_back(y);
		}
	}
	st.push(v[0][0]);
	for(int i=1;i<v[0].size();i++)
	{
		if(v[0][i]<st.top())
		{
			st.push(v[0][i]);
		}
		else
			st.push(st.top());
	}
	cin>>q;
	ll ind,k,val;
	int c=0;
	for(int i=0;i<q;i++)
	{
		cin>>ind;
		
		if(ind==1)
		{
			cin>>k>>val;
			k-=1;
			v[k].push_back(val);
			if(k==0)
			{
				
				if(val<st.top())
				{
					st.push(val);
				}
				else
				{
					st.push(st.top());
				}
			}
		}
		else if(ind==0)
		{
			cin>>k;
			k-=1;
			v[k].pop_back();
			if(k==0)
				st.pop();
		}
		else
		{
			if(check())
				cout<<"YES"<<endl;
			else
				cout<<"NO"<<endl;
		}
		
	}
	return 0;
}
```



