
**Q- Stock Span Problem**
In Stack notes.

**Q- Next Greater Element I**

Ex - 4 5 2 25
Ans- 5 25 25 -1

Ex - 10 7 4 2 9 10 11 3 2
Ans- 11 9 9 9 10 11 -1 -1 -1

Approach 1: Use two loops: The outer loop picks all the elements one by one. The inner loop looks for the first greater element for the element picked by the outer loop. If a greater element is found then that element is printed as next, otherwise -1 is printed.

Complexity: O(n^2)

Approach 2:
  Intuition:
  
  In case of a decreasing sequence, the answer is always going to be -1 for all elements till I dont encounter a increasing sequence/number. 
  For eg: 5 4 3 2 1
          -1 -1 -1 -1 -1
          
          5 4 3 2 1 10
          10 10 10 10 10 -1
          
          For all the elements less than 10 in a decreasing sequence are going to have the answer 10. 
          
          11 4 3 2 10 12
          
          Till 2, it is a decreasing sequence. After that, it is a increasing sequence then. So, for all the elements less than 10, the elements are going to have an answer 10. 
          Now the question is reduced to 11 10 12. Again 11 and 10 is a decreasing sequence, so the answer for them is going to be 12 12. 
          
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
                    System.out.println(element + " --> " + next); 
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
            System.out.println(element + " -- " + next); 
        } 
```
**Q-- Next Greater Element 2**

Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
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

**Q- Next Greater Element 3**

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. 
f
Input: [1,2,1]
Output: [2,-1,2]


**Q- Next Smaller Element 3**

**Q- Maximum area of a rectangle in a histogram**

**Q- Remove Duplicates and answer should be lexicographically smallest**

Input: bcabc
Output: abc

Input: cbacdcbc
Output: acdb

**Q- Decode an encrypted string**

**Q- Number of Valid Subarrays**
Given an array A of integers, return the number of non-empty continuous subarrays that satisfy the following condition:
The leftmost element of the subarray is not larger than other elements in the subarray.

Input: [1,4,2,5,3]
Output: 11
Explanation: There are 11 valid subarrays: [1],[4],[2],[5],[3],[1,4],[2,5],[1,4,2],[2,5,3],[1,4,2,5],[1,4,2,5,3].
 
```java 
public int validSubarrays(int[] nums) {
        int res = 0;
        Stack<Integer> stack = new Stack<>();
        for (int num : nums) {
            while (!stack.isEmpty() && num < stack.peek()) {
                stack.pop();
            }
            stack.push(num);
            res += stack.size();
        }
        return res;
    }
```


