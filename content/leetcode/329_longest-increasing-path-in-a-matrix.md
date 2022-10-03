---
weight: 329
title: "329 Longest Increasing Path in a Matrix"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_matrix", "lc_dfs", "lc_dp"]
---

Given an `m x n` integers `matrix`, return _the length of the longest increasing path in `matrix`_.

From each cell, you can either move in four directions: left, right, up, or down. You **may not** move **diagonally** or move **outside the boundary** (i.e., wrap-around is not allowed).

**Example 1:**
```

Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: The longest increasing path is [1, 2, 6, 9].
```
**Example 2:**
```

Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]
Output: 4
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```
**Example 3:**
```
Input: matrix = [[1]]
Output: 1
```

**Constraints:**
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- <code>0 <= matrix[i][j] <= 2<sup>31</sup> - 1</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        m, n = len(matrix), len(matrix[0])
        cache = collections.defaultdict(int) # [int, int] => int

        def dfs(i, j):
            if (i, j) in cache:
                return cache[(i, j)]
            for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                x, y = i + dx, j + dy
                if (
                    0 <= x < m and
                    0 <= y < n and
                    matrix[x][y] > matrix[i][j]
                ):
                    cache[(i, j)] = max(cache[(i, j)], dfs(x, y))
            cache[(i, j)] += 1
            return cache[(i, j)]
        
        ans = 0
        for i in range(m):
            for j in range(n):
                ans = max(ans, dfs(i, j))
        return ans
{{< / highlight >}}
</div>
</div>
