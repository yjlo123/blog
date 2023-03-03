---
weight: 279
title: "279 Perfect Squares"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp", "lc_bfs"]
---

Given an integer `n`, return *the least number of perfect square numbers that sum to `n`*.

A **perfect square** is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and `16` are perfect squares while `3` and `11` are not.


**Example 1:**
```
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```
**Example 2:**
```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

**Constraints:**
- <code>1 <= n <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [math.inf] * (n + 1)
        dp[0] = 0
        for i in range(1, n+1):
            j = 1
            while j*j <= i:
                dp[i] = min(dp[i], dp[i - j*j] + 1)
                j += 1
        return dp[n]
{{< / highlight >}}
</div>
</div>
