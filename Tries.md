### Tries

Situation: Rahul is a Software Engineer at Netflix. And he has been asked to implement the search functionality on the website. 

Tasks:
- Find the names of the all movies available on netflix and store them in a efficient manner. 
- Efficient Retrieval of the movie. If I type prefix, possible movie names should appear. 
For eg: term..
Suggestions: Terminator 1, Terminator 2, Terminator 3,....


**Task 1:**
Given a bag of words, containing all the movies, you need to store them efficiently. Design in such a way that add() functions and search() functions can be done efficiently. 
 Approach 1: HashMaps <Key, Value>
 	     Key: Movie Name
	     Value: Could be anything..
	     
	     Time Complexity: Let's say the length of the longest movie name is 'n'. Also, the movie names are made of only 		  of lowercase alphabets. Some movie lengths can be of length 1, 2, 3, 4, 5 ....
	     Total space: Space (1) + Space (2) + Space (3) + ...
	     Considering 1 character, taking 1 byte of space..
	     Space (1) = 1 x 26
	     Space (2) = 2 x 26 x 26
	     .
	     .
	     .
	     Space (n) = n X 26^n
	     
	     How can we optimise this?
	     
Approach 2: We can store the common things (prefix) together. **Need shared space for common variables.**
	    Form a tree kind of structure. Single instance of common prefix. 
		
	    Can we use stacks? Queues? 
	    Form a tree structure. Separate node for different movie names.
	    Time Complexity: Movie names: ape, appy, apple, apiapi
	   			26 + 26^2 +.........+ 26^n
	    Time complexity for storing is optimised. But in case of searching, it remains same. O(len(str))
	    
	    Let's say if I want to search for "api". api is not present, still we get true as answer.
	    So, we need one more check.
	    
```java
private class Node {
		char ch;
		boolean eow;
		HashMap<Character, Node> table;
	}
```

- Derived from - Re - Trie - val. 
- Need shared space for common variables. 

Functions: 
- Add()

```java

	public void addWord(Node parent, String word) {

		if (word.length() == 0) {
			if(!parent.eow) {
			 	parent.eow = true;
				return;
			}
		} 
		char ch = word.charAt(0);
		String row = word.substring(1);

		Node child = parent.table.get(ch);

		if (child == null) {
			child = new Node(ch);
			parent.table.put(ch, child);

		}	
		addWord(child, row);		
	}
```
- Search()

```java

	public boolean searchWord(Node parent, String word) {

		if (word.length() == 0) {
			return parent.eow;
		}

		char ch = word.charAt(0);
		String row = word.substring(1);

		Node child = parent.table.get(ch);

		if (child == null) {
			return false;
		} else {
			return searchWord(child, row);
		}
	}

```

Time Complexity to insert a new word: O(k)
Time Complexity to retrieve a word: O(k)

If solving using recursion: 
	Space Complexity: O(n)
	
**Q1- Given a set of words, find all the words with given prefix**
	Can be done easily now.
**Q2- Given a set of words, find all the words with given suffix**
	
**Q3- Given an array of words, convert it into a unique prefix array**
	
array = ["zebra", "dog", "dove", "duck"];
output = ["z", "dog", "dov", "du"];
	
Brute force Approach: Compare all prefixs of all words in array.
Time Complexity: O(n^2 x len(max(str)))
		
Optimised Approach: If a particular prefix is not unique, this means that it will be shared among more than 1 string. So why not keep a count on what are the number of strings in which a particular prefix is stored, and the prefix which is present only in one string will be unique. As we need prefix based calculation, a Trie(Prefix tree) will be helpful. At each node we can keep a count that the prefix ending at this node is shared among how many strings.

Now one way to tackle the above approach is to check for those nodes which have more than one child node because they will be showing sharing of a prefix into multiple words. But is this approach enough to cover all corner cases??

No, consider the case of [Zebra, Zebras]. Here the common prefix array will be [Zebra, Zebras]. Alhough the node 'a' is distributed with only single child still it will be unique common prefix.

So other way to handle this is to keep a freq parameter inside our trinode in order to keep a check on how many strings shared nodes till the current node.
		
**Q4- Maximum XOR pair**

![Screenshot 2020-01-20 at 7 30 22 PM](https://user-images.githubusercontent.com/35702912/72732287-5d645100-3bbb-11ea-86ad-8a16ef24d04e.png)

```cpp
class trieNode {
public:
	trieNode *left;
	trieNode *right;
};
class Solution {
public:
void insert(int n, trieNode *head) {
		trieNode *curr = head;
		for (int i = 31; i >= 0; i--) {
			int bit = (n >> i) & 1;
			if (bit == 0) {
				if (curr->left == NULL) {
					curr->left = new trieNode();
				}
				curr = curr->left;
			} else {
				if (curr->right == NULL) {
					curr->right = new trieNode();
				}
				curr = curr->right;
			}
		}
}

int findMaxXorPair(trieNode *head, int *arr, int n) {
		int max_xor = INT_MIN;
		for (int i = 0; i < n; i++) {
			trieNode *curr = head;
			int value = arr[i];
			int curr_xor = 0;
			for (int j = 31; j >= 0; j--) {
				int b = (value >> j) & 1;
				if (b == 0) {
					if (curr->right != NULL) {
						curr = curr->right;
						curr_xor += (int)pow(2, j);
					} else {
						curr = curr->left;
					}
				} else {
					if (curr->left != NULL) {
						curr = curr->left;
						curr_xor += (int)pow(2, j);
					} else {
						curr = curr->right;
					}
				}
			}
			if (curr_xor > max_xor) {
				max_xor = curr_xor;
			}
		}
		return max_xor;
}
    int findMaximumXOR(vector<int>& nums) {
       int n=nums.size();
	    int* arr = new int[n]();
	    for (int i = 0; i < n; i++) {
		    arr[i] = nums[i];
	    }
	    trieNode *head = new trieNode();
	    for (int i = 0; i < n; i++) {
	    	insert(arr[i], head);
	    } 
        return findMaxXorPair(head, arr, n);
    }
};

```
**Q5- Maximum XOR Subarray**

We know that by property of xor, lets say F(x, y) is a function that calculates the xor of an array from index x to index y, then we can deduce the equation like: 
F(x, y) = F(1, x - 1) ^ F(1, Y) (For all x < y )

Now having the above knowledge, lets say we have an array like [a,b,c,d,e,f]

We know that how to calculate a pair in the array such that it's xor is maximum. Now if you will carefully observe the above equation you will realise the fact that in order to calculate the subarray of any subarray, you can calculate it easily by having the prefix xor subarray values till X-1 and Y.

Lets convert the given array into prefix xor array like

[a, a^b, a^b^c, a^b^c^d, a^b^c^d^e, a^b^c^d^e^f]

Now can we find a pair in the above array such that it's xor is max???? Yes, we have done this question earlier.

Lets say the maximum xor pair is coming from index 2 and index 6 i.e. (a^b) ^ (a^b^c^d^e^f). Lets say this value is C. So C is the max xor pair value in the updated prefix xor array. Now if you will carefully visualize the value of C then you will get that C = (a^b) ^ (a^b^c^d^e^f) = a^b^a^b^c^d^e^f = c^d^e^f. And c^d^e^f is the xor of subarray [c,d,e,f] and as this is the max value so the subarray [c,d,e,f] will give max xor. 

Simple :-p

```java

import java.util.Scanner;

public class maxXorSubarray {

	public static class trieNode {
		trieNode left;
		trieNode right;
		int value;
	}

	public static void insert(int n, trieNode head) {
		trieNode curr = head;
		for (int i = 31; i >= 0; i--) {
			int bit = (n >> i) & 1;
			if (bit == 0) {
				if (curr.left == null) {
					curr.left = new trieNode();
				}
				curr = curr.left;
			} else {
				if (curr.right == null) {
					curr.right = new trieNode();
				}
				curr = curr.right;
			}
		}
		curr.value = n;
	}

	public static int query(trieNode head, int value, int n) {
		int max_xor = Integer.MIN_VALUE;
		trieNode curr = head;
		int curr_xor = 0;
		for (int j = 31; j >= 0; j--) {
			int b = (value >> j) & 1;
			if (b == 0) {
				if (curr.right != null) {
					curr = curr.right;
				} else {
					curr = curr.left;
				}
			} else {
				if (curr.left != null) {
					curr = curr.left;
				} else {
					curr = curr.right;
				}
			}
		}
		return value^curr.value;
	}

	public static void main(String[] args) {

		Scanner scn = new Scanner(System.in);
		int n = scn.nextInt();
		int[] arr = new int[n];
		for (int i = 0; i < arr.length; i++) {
			arr[i] = scn.nextInt();
		}
		int pre_xor = 0;
		int result = Integer.MIN_VALUE;
		trieNode head = new trieNode();
		for (int i = 0; i < arr.length; i++) {
			pre_xor ^= arr[i];
			insert(pre_xor, head);
			result = Math.max(result, query(head, pre_xor, n));
		}
		System.out.println(result);
	}

}
```

**Q6- Word Search**

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

![Screenshot 2020-01-20 at 3 11 05 PM](https://user-images.githubusercontent.com/35702912/72732288-5e957e00-3bbb-11ea-986e-5730c6141a40.png)



```cpp

class TrieNode {
public:
    char ch;
    bool isTerminal;
    unordered_map<char, TrieNode*> children;
    TrieNode(char ch, bool isTerminal) {
        this->ch = ch;
        this->isTerminal = isTerminal;
    }
    
};
class Solution {
public:
    vector<string> result;
    void insert(string word, TrieNode *root) {
        TrieNode* temp = root;
        for(int i = 0; i < word.size(); i++) {
            char ch = word[i];
            if(temp->children.find(ch) != temp->children.end()) {
                temp = temp->children[ch];
            } else {
                temp->children[ch] = new TrieNode(ch, false);
                temp = temp->children[ch];
            }
        }
        temp->isTerminal = true;
        return;
    }
    
    
    void backtrack(vector<vector<char>>& board, TrieNode* root, int i, int j, bool **visited, string str) {
        if(i < 0 or j < 0 or i >= board.size() or j >= board[0].size()) {
            return;
        }
        if(visited[i][j] == true) return;
        char ch = board[i][j];
        if(root->children.find(ch) == root->children.end()) {
            return;
        } else {
            root = root->children[ch];
        }
        if(root->isTerminal == true) {
            result.push_back(str+board[i][j]);
            root->isTerminal = false;
        }
        visited[i][j] = true;
        backtrack(board, root, i+1, j, visited, str+board[i][j]);
        backtrack(board, root, i-1, j, visited, str+board[i][j]);
        backtrack(board, root, i, j+1, visited, str+board[i][j]);
        backtrack(board, root, i, j-1, visited, str+board[i][j]);
        visited[i][j] = false;
        return;
    }
    
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        TrieNode *root = new TrieNode('\0', false);
        for(string word: words) {
            insert(word, root);
        }
        bool **visited = new bool*[board.size()];
        for(int i = 0; i < board.size(); i++) {
            visited[i] = new bool[board[0].size()]();
        }
        
        for(int i = 0; i < board.size(); i++) {
            for(int j = 0; j < board[0].size(); j++) {
                TrieNode* temp = root;
                backtrack(board, temp, i, j, visited, "");
            }
        }
        return result;
    }
};

```

 **Homework Problem**
 
 https://www.codechef.com/problems/SUBBXOR
