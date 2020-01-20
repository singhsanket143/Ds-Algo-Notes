### Tries


- Derived - Re - Trie - val
- Need shared space for common variables. 
- Example: Autocomplete System

Time Complexity to insert a new word: O(k)
Time Complexity to retrieve a word: O(k)


**Q1- Given a set of words, find all the words with given prefix**

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
