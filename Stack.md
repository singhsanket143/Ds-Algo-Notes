
## Stack

- Abstract Datatype
 Integers are also abstract datatype. 
 
### Stack Operations
- Push
- Pop
### Implementation of Stack
- Array (Keep the two conditions in mind during interviews)
  - Stack Overflow
  - Stack Underflow
- LinkedList
- Queue

### Application of Stack
- Recursion
- Undo/Redo
  Example of Calculator - Maintain Two Stacks
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

Similar to above question. Just implement insertInSortedWay(). 

**Q- Implement getMin() function**
Approach 1: 
Using another stack.  
- O(n) Space Complexity

Approach 2: 
- O(1) Space Complexity

**Q- Implement getMin() function**

**Q- Remove duplicates in a string**

**Q- Valid Paranthesis**

**Q- Stock Span Problem**

**Q- Next Greater Element**







