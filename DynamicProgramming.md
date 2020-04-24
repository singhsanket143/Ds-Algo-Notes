If a problem is having the following two properties then it's classified as a DP problem
- Optimal Substructure
- Overlapping Subproblem

Q- What is optimal substructure? 
Ans: It means that you can divide a bigger problem to smaller subproblem, and you aggregate the answers of the smaller subproblem, you will get the answer for the bigger problem i.e. if we use optimal answers of smaller subproblems then the bigger problem will also be solved optimally.

Q- What is iverlapping subproblem?
Ans: If the number of unique states of a problem is less than the total number of states then the problem is said to have overlapping subproblem

-> Discuss element of choice
-> TC - No of uniq states * time it takes to solve one state

**Q: Discuss Fibonacci problem.**

**Q:House robber**
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.


Input: [2,7,9,3,1]
Output: 12
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.

Solution: 
It could be overwhelming thinking of all possibilities on which houses to rob.

A natural way to approach this problem is to work on the simplest case first.

Let us denote that:

f(k) = Largest amount that you can rob from the first k houses.
Ai = Amount of money at the ith house.

Let us look at the case n = 1, clearly f(1) = A1.

Now, let us look at n = 2, which f(2) = max(A1, A2).

For n = 3, you have basically the following two options:

Rob the third house, and add its amount to the first house's amount.

Do not rob the third house, and stick with the maximum amount of the first two houses.

Clearly, you would want to choose the larger of the two options at each step.

Therefore, we could summarize the formula as following:
f(k) = max(f(k – 2) + Ak, f(k – 1))
We choose the base case as f(–1) = f(0) = 0, which will greatly simplify our code as you can see.

The answer will be calculated as f(n). We could use an array to store and calculate the result, but since at each step you only need the previous two maximum values, two variables are suffice.

**Q: Party Problem**

**Q: Decode Ways**
A message containing letters from A-Z is being encoded to numbers using the following mapping:
'A' -> 1
'B' -> 2
...
'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).

Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).


A cell with index i of the dp array is used to store the number of decode ways for substring of s from index 0 to index i-1.

```java
class Solution {

    public int numDecodings(String s) {

        if(s == null || s.length() == 0) {
            return 0;
        }

        // DP array to store the subproblem results
        int[] dp = new int[s.length() + 1];
        dp[0] = 1;
        // Ways to decode a string of size 1 is 1. Unless the string is '0'.
        // '0' doesn't have a single digit decode.
        dp[1] = s.charAt(0) == '0' ? 0 : 1;

        for(int i = 2; i < dp.length; i += 1) {

            // Check if successful single digit decode is possible.
            if(s.charAt(i-1) != '0') {
               dp[i] += dp[i-1];  
            }

            // Check if successful two digit decode is possible.
            int twoDigit = Integer.valueOf(s.substring(i-2, i));
            if(twoDigit >= 10 && twoDigit <= 26) {
                dp[i] += dp[i-2];
            }
        }
        return dp[s.length()];

    }
}
```
**Q: Coin Change**
You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
Example 2:

Input: coins = [2], amount = 3
Output: -1

```java
public int coinChange(int[] coins, int amount) {
        int n = coins.length;
        int ans = -1;
        int[] dp = new int[amount + 1];
        for (int i = 1; i <= amount; i++) {
            dp[i] = Integer.MAX_VALUE;
            for (int j = 0; j < n; j++) {
                if (coins[j] > i) continue;
                if (dp[i - coins[j]] == Integer.MAX_VALUE) continue;
                dp[i] = Math.min(dp[i], 1 + dp[i - coins[j]]);
            }
        }
        return (dp[amount] == Integer.MAX_VALUE) ? -1 : dp[amount];
    }
```

**Q: Minimum Number of Squares**
Given an integer N. Return count of minimum numbers, sum of whose squares is equal to N.

Example:

N=6

Possible combinations are :

(12 + 12 + 12 + 12 + 12 + 12)
(12 + 12 + 22)
So, minimum count of numbers is 3 (i.e. 1,1,2).

Note:

1 ≤ N ≤ 10^5
