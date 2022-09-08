---
weight: 994
title: "994 Rotting Oranges"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bfs", "lc_matrix"]
---

You are given an `m x n` grid where each cell can have one of three values:
- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return _the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`_.

**Example 1:**
```
  0          1          2          3          4
2 1 1      2 2 1      2 2 2      2 2 2      2 2 2
1 1 0  =>  2 1 0  =>  2 2 0  =>  2 2 0  =>  2 2 0
0 1 1      0 1 1      0 1 1      0 2 1      0 2 2

Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```
**Example 2:**
```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten,
because rotting only happens 4-directionally.
```
**Example 3:**
```
Input: grid = [[0,2]]
Output: 0
Explanation: Since there are already no fresh oranges at minute 0,
the answer is just 0.
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j]` is `0`, `1`, or `2`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        q = deque()
        m, n = len(grid), len(grid[0])
        total = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 2:
                    q.append((i, j))
                if grid[i][j] > 0:
                    total += 1
        if total == 0:
            return 0
        
        minute = -1
        count = 0
        while q:
            minute += 1
            q_size = len(q)
            for _ in range(q_size):
                count += 1
                (x, y) = q.popleft()
                for d in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                    x2 = x + d[0]
                    y2 = y + d[1]
                    if (
                        0 <= x2 < m
                        and 0 <= y2 < n
                        and grid[x2][y2] == 1
                    ):
                        q.append((x2, y2))
                        grid[x2][y2] = 2
        return minute if count == total else -1
{{< / highlight >}}
</div>
</div>
