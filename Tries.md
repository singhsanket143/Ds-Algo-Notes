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
	
**Q4- Maximum XOR pair**

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
