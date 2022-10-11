---
weight: 934
title: "934 Shortest Bridge"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_dfs", "lc_bfs"]
---

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An **island** is a 4-directionally connected group of `1`'s not connected to any other `1`'s. There are exactly two islands in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form **one island**.

Return _the smallest number of `0`'s you must flip to connect the two islands_.

**Example 1:**
```
Input: grid = [
    [0,1],
    [1,0]
]
Output: 1
```
**Example 2:**
```
Input: grid = [
    [0,1,0],
    [0,0,0],
    [0,0,1]
]
Output: 2
```
**Example 3:**
```
Input: grid = [
    [1,1,1,1,1],
    [1,0,0,0,1],
    [1,0,1,0,1],
    [1,0,0,0,1],
    [1,1,1,1,1]
]
Output: 1
```

**Constraints:**
- `n == grid.length == grid[i].length`
- `2 <= n <= 100`
- `grid[i][j]` is either `0` or `1`.
- There are exactly two islands in `grid`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def shortestBridge(self, grid: List[List[int]]) -> int:
        n = len(grid)
        DIRS = [(1, 0), (-1, 0), (0, 1), (0, -1)]

        def find_island() -> Tuple[int, int]:
            for i in range(n):
                for j in range(n):
                    if grid[i][j] == 1:
                        return i, j
            return -1, -1

        def dfs(i: int, j: int, q: List[Tuple[int, int]]) -> None:
            grid[i][j] = -1
            # add to q, used by BFS
            q.append((i, j))
            for dx, dy in DIRS:
                x, y = i + dx, j + dy
                if 0 <= x < n and 0 <= y < n and grid[x][y] == 1:
                    dfs(x, y, q)
        
        step = 0
        q = []
        ix, iy = find_island()
        dfs(ix, iy, q)

        # expand the found island using BFS
        while q:
            temp_q = []
            for i, j in q:
                for dx, dy in DIRS:
                    x, y = i + dx, j + dy
                    if 0 <= x < n and 0 <= y < n:
                        if grid[x][y] == 1:
                            return step
                        elif grid[x][y] == 0:
                            grid[x][y] = -1
                            temp_q.append((x, y))
            step += 1
            q = temp_q
        return -1
{{< / highlight >}}
</div>
</div>
