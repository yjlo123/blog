---
weight: 1293
title: "1293 Shortest Path in a Grid with Obstacles Elimination"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_bfs"]
---

You are given an `m x n` integer matrix `grid` where each cell is either `0` (empty) or `1` (obstacle). You can move up, down, left, or right from and to an empty cell in **one step**.

Return _the minimum number of steps to walk from the upper left corner `(0, 0)` to the lower right corner `(m - 1, n - 1)` given that you can eliminate at most k obstacles_. If it is not possible to find such walk return `-1`.

**Example 1:**
```
_ _ _
# # _
_ _ _
_ # #
_ _ _

Input: grid = [
    [0,0,0],
    [1,1,0],
    [0,0,0],
    [0,1,1],
    [0,0,0]
], k = 1
Output: 6
Explanation: 
The shortest path without eliminating any obstacle is 10.
The shortest path with one obstacle elimination at position (3,2) is 6. Such path is (0,0) -> (0,1) -> (0,2) -> (1,2) -> (2,2) -> (3,2) -> (4,2).
```
**Example 2:**
```
_ # #
# # #
# _ _

Input: grid = [
    [0,1,1],
    [1,1,1],
    [1,0,0]
], k = 1
Output: -1
Explanation: We need to eliminate at least two obstacles to find such a walk.
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 40`
- `1 <= k <= m * n`
- `grid[i][j]` is either `0` **or** `1`.
- `grid[0][0] == grid[m - 1][n - 1] == 0`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        m = len(grid)
        n = len(grid[0])

        if k >= m + n - 2:
            return m + n -2

        state = (0, 0, k)
        q = deque([(0, state)])
        seen = set([state])

        while q:
            steps, (i, j, k) = q.popleft()

            if (i, j) == (m-1, n-1):
                return steps

            for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                x, y = i + dx, j + dy
                if 0 <= x < m and 0 <= y < n:
                    nk = k - grid[x][y]
                    new_state = (x, y, nk)
                    if nk >= 0 and new_state not in seen:
                        seen.add(new_state)
                        q.append((steps + 1, new_state))

        return -1
{{< / highlight >}}
</div>
</div>
