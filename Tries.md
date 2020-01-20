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

**Q6- Word Search**

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

 **Homework Problem**
 
 https://www.codechef.com/problems/SUBBXOR
