---
weight: 634
title: "634 Find the Derangement of An Array"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

In combinatorial mathematics, a **derangement** is a permutation of the elements of a set, such that no element appears in its original position.

You are given an integer `n`. There is originally an array consisting of `n` integers from `1` to `n` in ascending order, return _the number of **derangements** it can generate_. Since the answer may be huge, return it **modulo** <code>10<sup>9</sup> + 7</code>.

**Example 1:**
```
Input: n = 3
Output: 2
Explanation: The original array is [1,2,3].
The two derangements are [2,3,1] and [3,1,2].
```
**Example 2:**
```
Input: n = 2
Output: 1
```

**Constraints:**
- <code>1 <= n <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findDerangement(self, n: int) -> int:
        MOD = 10**9+7
        dp = [0, 1]
        if n <= 2:
            return dp[n - 1] 
        for i in range(3, n+1):
            j = (dp[0] + dp[1]) * (i - 1) % MOD
            dp[0] = dp[1]
            dp[1] = j
        return dp[-1]
{{< / highlight >}}
</div>
</div>
