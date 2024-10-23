# Palindromic Substrings
Given a string s, return the number of palindromic substrings in it.
A string is a palindrome when it reads the same backward as forward.
A substring is a contiguous sequence of characters within the string.

```
Example 1:

Input: s = "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".

Example 2:

Input: s = "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
``` 

## Constraints:

1. 1 <= s.length <= 1000
2. s consists of lowercase English letters.

# Implementation 1 : Dynamic Programming, Time = O(n^2), Space = O(n^2)
```java
class Solution {
    public int countSubstrings(String s) {
        int n = s.length(), ans = 0;
        if (n == 0) 
            return 0;

        boolean[][] dp = new boolean[n][n];
        // Base case: single letter substrings
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            ans++;
        }
        // Base case: double letter substrings
        for (int i = 0; i < n - 1; i++) {
            dp[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
            ans += (dp[i][i + 1] ? 1 : 0);
        }
        // All other cases: substrings of length 3 to n
        for (int len = 3; len <= n; len++) {
            for (int i = 0, j = i + len - 1; j < n; i++, j++) {
                dp[i][j] = (s.charAt(i) == s.charAt(j)) && dp[i + 1][j - 1];
                ans += (dp[i][j] ? 1 : 0);
            }
        }
        return ans;
    }
}
```

# References :
1. https://www.youtube.com/watch?v=XmSOWnL6T_I
2. https://leetcode.com/problems/palindromic-substrings/editorial
