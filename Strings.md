
**Q1- First Unique Character in a String** 

**Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.**

```
s = "InterviewBit"
return 1.
```

_Approach:_

The best possible solution here could be of a linear time because to ensure that the character is unique you have to check the whole string anyway.

The idea is to go through the string and save in a hash map the number of times each character appears in the string. That would take O(N) time, where N is a number of characters in the string.

And then we go through the string the second time, this time we use the hash map as a reference to check if a character is unique or not.
If the character is unique, one could just return its index. The complexity of the second iteration is O(N) as well.

```
public int firstUniqChar(String s) {
        HashMap<Character, Integer> count = new HashMap<Character, Integer>();
        int n = s.length();
        // build hash map : character and how often it appears
        for (int i = 0; i < n; i++) {
            char c = s.charAt(i);
            count.put(c, count.getOrDefault(c, 0) + 1);
        }
        
        // find the index
        for (int i = 0; i < n; i++) {
            if (count.get(s.charAt(i)) == 1) 
                return i;
        }
        return -1;
```

Time complexity : O(N) since we go through the string of length N two times.

Space complexity : O(N) since we have to keep a hash map with N elements.

**Q2- Isomorphic Strings**

**Given two strings s and t, determine if they are isomorphic.Two strings are isomorphic if the characters in s can be replaced to get t. All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.**

```
Input: s = "egg", t = "add"
Output: true

Input: s = "foo", t = "bar"
Output: false

Input: s = "paper", t = "title"
Output: true
```

**Q3- Valid Anagram**

**Given two strings s and t , write a function to determine if t is an anagram of s.**

```
Input: s = "anagram", t = "nagaram"
Output: true

Input: s = "rat", t = "car"
Output: false
```

**Q4- Check if a string can be obtained by rotating another string 2 places**

```
Input: string1 = “amazon”, string2 = “azonam”
Output: Yes
// rotated anti-clockwise

Input: string1 = “amazon”, string2 = “onamaz”
Output: Yes
// rotated clockwise
```

1- There can be only two cases:
    a) Clockwise rotated
    b) Anti-clockwise rotated

2- If clockwise rotated that means elements
   are shifted in right.
   So, check if a substring[2.... len-1] of 
   string2 when concatenated with substring[0,1]
   of string2 is equal to string1. Then, return true.

3- Else, check if it is rotated anti-clockwise 
   that means elements are shifted to left.
   So, check if concatenation of substring[len-2, len-1]
   with substring[0....len-3] makes it equals to
   string1. Then return true.

4- Else, return false.

```
static boolean isRotated(String str1, String str2) 
    { 
        if (str1.length() != str2.length()) 
            return false; 
       
        String clock_rot = ""; 
        String anticlock_rot = ""; 
        int len = str2.length(); 
       
        // Initialize string as anti-clockwise rotation 
        anticlock_rot = anticlock_rot + 
                        str2.substring(len-2, len) + 
                        str2.substring(0, len-2) ; 
       
        // Initialize string as clock wise rotation 
        clock_rot = clock_rot + 
                    str2.substring(2) + 
                    str2.substring(0, 2) ; 
       
        // check if any of them is equal to string1 
        return (str1.equals(clock_rot) || 
                str1.equals(anticlock_rot)); 
    } 
    
    
```

**Q5- Given an input string, reverse the string word by word.**

```
Input: "the sky is blue"
Output: "blue is sky the"

Input: "  hello world!  "
Output: "world! hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

- A word is defined as a sequence of non-space characters.

- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.

- You need to reduce multiple spaces between two words to a single space in the reversed string.

https://leetcode.com/problems/reverse-words-in-a-string/solution/

**Q6- String to Integer (atoi)**

https://leetcode.com/problems/string-to-integer-atoi/

**Q7- Longest Substring Without Repeating Characters**

**Given a string, find the length of the longest substring without repeating characters.**
```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

https://leetcode.com/problems/longest-substring-without-repeating-characters/solution/

**Homework Problem**

https://codeforces.com/problemset/problem/676/C
 
