
**Q1- Implement getMin() function**

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


For inital example: 16, 15, 29, 14, 18

Stack: 16, -1, 29, -1, 18 

Improved: 16, 15, -13, 12 

Stack: 16, 14, -41, 12

**Q2- Evaluate Infix Expression**

1. Maintain two stacks, one for integers and one for operators

```java
         //Stack for numbers
         Stack<Integer> numbers = new Stack<>();

        //Stack for operators
        Stack<Character> operations = new Stack<>();
        
        for(int i=0; i<expression.length();i++) {
            char c = expression.charAt(i);
            
            //check if it is number
            if(Character.isDigit(c)){
                //Entry is Digit, it could be greater than one digit number
                int num = 0;
                while (Character.isDigit(c)) {
                    num = num*10 + (c-'0');
                    i++;
                    if(i < expression.length())
                        c = expression.charAt(i);
                    else
                        break;
                }
                i--;
                //push it into stack
                numbers.push(num);
            }else if(c=='('){
                //push it to operators stack
                operations.push(c);
            }
            
            
            else if(c==')') {
                while(operations.peek()!='('){
                    int output = performOperation(numbers, operations);
                    numbers.push(output);
                }
                operations.pop();
            }
            // current character is operator
            else if(isOperator(c)){
                operations.push(c);
            }
        }

        while(!operations.isEmpty()){
            int output = performOperation(numbers, operations);
            numbers.push(output);
        }
        return numbers.pop();
    }

    public int performOperation(Stack<Integer> numbers, Stack<Character> operations) {
        int a = numbers.pop();
        int b = numbers.pop();
        char operation = operations.pop();
        switch (operation) {
            case '+':
                return a + b;
            case '-':
                return b - a;
            case '*':
                return a * b;
            case '/':
                if (a == 0)
                    throw new
                            UnsupportedOperationException("Cannot divide by zero");
                return b / a;
        }
        return 0;
    }

    public boolean isOperator(char c){
        return (c=='+'||c=='-'||c=='/'||c=='*'||c=='^');
    }
```

Time Complexity: O(n)

Space Complexity: O(n)


**Q3- Next Smaller Element**

**Q4- Maximum area of a rectangle in a histogram**
Input: 7 bars of heights {6, 2, 5, 4, 5, 1, 6}
Output: Max Area = 12

**Q5- Maximal Rectangle**
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6

```java
public int leetcode84(int[] heights) {
        Stack < Integer > stack = new Stack < > ();
        stack.push(-1);
        int maxarea = 0;
        for (int i = 0; i < heights.length; ++i) {
            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i])
                maxarea = Math.max(maxarea, heights[stack.pop()] * (i - stack.peek() - 1));
            stack.push(i);
        }
        while (stack.peek() != -1)
            maxarea = Math.max(maxarea, heights[stack.pop()] * (heights.length - stack.peek() -1));
        return maxarea;
    }

    public int maximalRectangle(char[][] matrix) {

        if (matrix.length == 0) return 0;
        int maxarea = 0;
        int[] dp = new int[matrix[0].length];

        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {

                // update the state of this row's histogram using the last row's histogram
                // by keeping track of the number of consecutive ones

                dp[j] = matrix[i][j] == '1' ? dp[j] + 1 : 0;
            }
            // update maxarea with the maximum area from this row's histogram
            maxarea = Math.max(maxarea, leetcode84(dp));
        } return maxarea;
    }
  
```

**Q6- Remove Duplicates and answer should be lexicographically smallest**

Input: bcabc
Output: abc

Input: cbacdcbc
Output: acdb

For bab, you always want to remove the first b, because it is followed by a smaller character. 

Now here we need to check 3 condiions:
 - If we have already included a character and again the same occurs in our string then we won't consider it. How to achieve this??? Using a visited map
 - If for an index i, if the character at i+1 is greater than character ar i, and the character at i+1 is not already visited, we will include in our ans by pushing over stack.
 - Now for an index i, if the character at i+1 is smaller than that of at i, we will check that if the character at i, is going to be encounterted again to the right of i+1 or not. If not then do nothing, if yes then pop it our and wait for it's most significant spot to come.
 
 How to check if a character is present later on or not????? Using a frequency map and after each iteration update it, this will show that after an iteration on a string how many characters are still left .
 
```java
class Solution {
    public String removeDuplicateLetters(String s) {

        Stack<Character> stack = new Stack<>();

        // this lets us keep track of what's in our solution in O(1) time
        HashSet<Character> seen = new HashSet<>();

        // this will let us know if there are any more instances of s[i] left in s
        HashMap<Character, Integer> last_occurrence = new HashMap<>();
        for(int i = 0; i < s.length(); i++) last_occurrence.put(s.charAt(i), i);

        for(int i = 0; i < s.length(); i++){
            char c = s.charAt(i);
            // we can only try to add c if it's not already in our solution
            // this is to maintain only one of each character
            if (!seen.contains(c)){
                // if the last letter in our solution:
                //     1. exists
                //     2. is greater than c so removing it will make the string smaller
                //     3. it's not the last occurrence
                // we remove it from the solution to keep the solution optimal
                while(!stack.isEmpty() && c < stack.peek() && last_occurrence.get(stack.peek()) > i){
                    seen.remove(stack.pop());
                }
                seen.add(c);
                stack.push(c);
            }
        }
    StringBuilder sb = new StringBuilder(stack.size());
    for (Character c : stack) sb.append(c.charValue());
    return sb.toString();
    }
}
```
Time Complexity: 0(length of string)
Space Complexity: 0(1)

**Q7- Decode an encrypted string**

Given a String A and an integer B. String A is encoded consisting of lowercase English letters and numbers. A is encoded
in a way where repetitions of substrings are represented as substring followed by the count of substrings.

Input: “ab2c3” k = 8
Output: ababc ababc ababc  "a"

You have to find and return the Bth character in the decrypted string.

Note: Frequency of encrypted substring can be of more than one digit. For example,
in “ab12c3”, ab is repeated 12 times. No leading 0 is present in the frequency of substring.

Approach: We dont care about the characters that occur after k? Lets see how we can solve it without expanding the string. Do we see a pattern in this string? String repeated thrice. Lets say I have a string of substring length 5 which is repeated n times, then can we find the kth character by (k%5) i.e., (8%5) = 3. Now find 3rd character in ababc. We see again a pattern in this. A repeated subtring of length 2. So, now find 3%2. 

((((1+1) * 2) + 1)*3)
```cpp
string Solution::solve(string A, int B) {
    stack < pair<string, int > > st;
    int i, n = A.size();
    int len = 0;
    int num;
    int k = B;
    string curr;
    string temp = "";
    for(i=0; i<n; i++){
        if(A[i] >= 'a' && A[i] <= 'z'){
            len++;
            curr = A[i];
            st.push({curr, len});
        }else{
            num = 0;
            while(i < n && A[i] >= '0' && A[i] <= '9'){
                num = num*10;
                num += A[i]-'0';
                i++;
            }
            if(len*num >= k){
                break;
            }
            len = len*num;
            i--;
        }
    }
    pair <string, int> p;
    while(!st.empty()){
        p = st.top();
        st.pop();
        
        k = k%p.second;
        if(k == 0){
          return p.first;
        }
    }
}

Time Complexity: 0(length of string)
Space Complexity: 0(length of string)

```
**Q8- Number of Valid Subarrays**

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
Time Complexity: O(n) 
Space Complexity: O(n)

**Homework Problems**

http://codeforces.com/contest/797/problem/c


```java
#include<iostream>
#include<cstdio>
#include<cstring>
#include<stack>
using namespace std;
const int N=1e5+5;
int main()
{
    char s[N];
    gets(s);
    int n=strlen(s);
    char best[N];
    best[n]='z';
    for(int i=n-1;i>=0;i--)
    {
        best[i]=min(best[i+1],s[i]);
    }
    stack<char>v;
    int cur=0;
    while(!v.empty()||cur<n)
    {
        if(!v.empty()&&v.top()<=best[cur])
        {
            putchar(v.top());
             v.pop();
        }
        else v.push(s[cur++]);
    } 
    cout<<endl;
    return 0;
}
```
Time Complexity: O(n)
Space Complexity: O(n)
