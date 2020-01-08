
## Stack
- Abstract Datatype
 Integers are also abstract datatype. 
- Linear data structure 
- LIFO (Last In First Out)

### Stack Operations
- Push
- Pop
### Implementation of Stack
- Array (Keep the two conditions in mind during interviews)
  - Stack Overflow
  - Stack Underflow
  - **Pros**: Easy to implement. Memory is saved as pointers are not involved.
  - **Cons**: It is not dynamic. It doesn’t grow and shrink depending on needs at runtime.
- LinkedList
  - Push() - Add at head. O(1)
  - Pop() - Remove at Head. O(1)
- Queue

### Application of Stack
- Recursion
- Undo/Redo
- Arithmetic Expression Evaluation
  Prefix  +ab
  Infix   a+b
  Postfix ab+
  
- Using factorial example, explain callstack.
- Iterative code better than recursion because you might run out of memory space. 

**Q- Given only two operations i.e., push() and pop(), implement insertAtBottom() function**
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

**Q- Reverse a stack** 
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

  Time Complexity - 
  Pushing one element at the bottom - O(n)
  Pushing n elements at the bottom - O(n^2)

Approach 2: Take two auxillary stack


**Q- Implement Sorting using stack**
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



**Q- Implement getMin() function**
Approach 1: 
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

Approach 2: 

Space Complexity: O(1)
Time Complexity: O(1)


**Q- Remove duplicates in a string**

**Q- Valid Paranthesis**

Input: "()[]{}"
Output: true

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

**Q- Stock Span Problem**

**Q- Next Greater Element**

**Q- Remove Duplicate Letters**








