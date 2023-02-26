---
weight: 1155
title: "1155 Number of Dice Rolls With Target Sum"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

You have `n` dice, and each die has `k` faces numbered from `1` to `k`.

Given three integers `n`, `k`, and `target`, return *the number of possible ways (out of the <code>k<sup>n</sup></code> total ways) to roll the dice, so the sum of the face-up numbers equals `target`*. Since the answer may be too large, return it modulo <code>10<sup>9</sup> + 7</code>.


**Example 1:**
```
Input: n = 1, k = 6, target = 3
Output: 1
Explanation: You throw one die with 6 faces.
There is only one way to get a sum of 3.
```
**Example 2:**
```
Input: n = 2, k = 6, target = 7
Output: 6
Explanation: You throw two dice, each with 6 faces.
There are 6 ways to get a sum of 7: 1+6, 2+5, 3+4, 4+3, 5+2, 6+1.
```
**Example 3:**
```
Input: n = 30, k = 30, target = 500
Output: 222616187
Explanation: The answer must be returned modulo 109 + 7.
```

**Constraints:**
- `1 <= n, k <= 30`
- `1 <= target <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        MOD = 10 ** 9 + 7
        dp = [[0] * (target + 1) for _ in range(2)]

        for i in range(1, min(k, target)+1):
            dp[0][i] = 1

        for i in range(1, n):
            r = i % 2
            p = (i-1) % 2
            for j in range(i-1, target+1):
                # start from (i-1) since impossible to get sum
                # of j < i with i dices
                current = 0
                for l in range(max(1, j - k), j):
                    current += dp[p][l]
                dp[r][j] = current

        return dp[(n-1) % 2][-1] % MOD
{{< / highlight >}}
</div>
</div>
