---
weight: 1143
title: "1143 Longest Common Subsequence"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

Given two strings `text1` and `text2`, return _the length of their longest **common subsequence**_. If there is no **common subsequence**, return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

**Example 1:**
```
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```
**Example 2:**
```
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
```
**Example 3:**
```
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
```

**Constraints:**
- `1 <= text1.length, text2.length <= 1000`
- `text1` and `text2` consist of only lowercase English characters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1)+1, len(text2)+1
        dp = [[0] * n for _ in range(2)]
        for i in range(1, m):
            ri = i % 2
            pi = (i - 1) % 2
            for j in range(1, n):
                if text1[i-1] == text2[j-1]:
                    dp[ri][j] = 1 + dp[pi][j-1]
                else:
                    dp[ri][j] = max(dp[pi][j], dp[ri][j-1])
        return dp[(m-1) % 2][-1]
{{< / highlight >}}
</div>
</div>
