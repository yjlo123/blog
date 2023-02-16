---
weight: 2435
title: "2435 Paths in Matrix Whose Sum Is Divisible by K"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_matrix", "lc_dp"]
---

You are given a **0-indexed** `m x n` integer matrix `grid` and an integer `k`. You are currently at position `(0, 0)` and you want to reach position `(m - 1, n - 1)` moving only **down** or **right**.

Return *the number of paths where the sum of the elements on the path is divisible by `k`*. Since the answer may be very large, return it **modulo** <code>10<sup>9</sup> + 7</code>.


**Example 1:**
```

Input: grid = [[5,2,4],[3,0,5],[0,7,2]], k = 3
Output: 2
Explanation: There are two paths where the sum of the elements on the path is
divisible by k.
The first path highlighted in red has a sum of 5 + 2 + 4 + 5 + 2 = 18
which is divisible by 3.
The second path highlighted in blue has a sum of 5 + 3 + 0 + 5 + 2 = 15
which is divisible by 3.
```
**Example 2:**
```

Input: grid = [[0,0]], k = 5
Output: 1
Explanation: The path highlighted in red has a sum of 0 + 0 = 0
which is divisible by 5.
```
**Example 3:**
```

Input: grid = [[7,3,4,9],[2,3,6,2],[2,3,7,0]], k = 1
Output: 10
Explanation: Every integer is divisible by 1 so the sum of the elementson every
possible path is divisible by k.
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- <code>1 <= m, n <= 5 * 10<sup>4</sup></code>
- <code>1 <= m * n <= 5 * 10<sup>4</sup></code>
- `0 <= grid[i][j] <= 100`
- `1 <= k <= 50`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberOfPaths(self, grid: List[List[int]], k: int) -> int:
        m, n = len(grid), len(grid[0])
        MOD = 10 ** 9 + 7

        dp = [[[0] * k for _ in range(n+1)] for _ in range(2)]

        for i in range(1, m+1):
            r = i % 2
            for j in range(1, n+1):
                if i == 1 and j == 1:
                    dp[1][1][grid[0][0] % k] = 1
                    continue
                top = dp[(i-1) % 2][j]
                left = dp[r][j-1]
                for x in range(k):
                    d = (x + grid[i-1][j-1]) % k
                    dp[r][j][d] = (top[x] + left[x])
                    dp[r][j][d] %= MOD
        return dp[m % 2][-1][0]
{{< / highlight >}}
</div>
</div>
