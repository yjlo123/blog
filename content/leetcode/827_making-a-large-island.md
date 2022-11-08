---
weight: 827
title: "827 Making A Large Island"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_matrix", "lc_dfs"]
---

You are given an `n x n` binary matrix `grid`. You are allowed to change **at most one** `0` to be `1`.

Return _the size of the largest **island** in `grid` after applying this operation_.

An **island** is a 4-directionally connected group of `1`s.


**Example 1:**
```
Input: grid = [[1,0],[0,1]]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s,
then we get an island with area = 3.
```
**Example 2:**
```
Input: grid = [[1,1],[1,0]]
Output: 4
Explanation: Change the 0 to 1 and make the island bigger,
only one island with area = 4.
```
**Example 3:**
```
Input: grid = [[1,1],[1,1]]
Output: 4
Explanation: Can't change any 0 to 1,
only one island with area = 4.
```

**Constraints:**
- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 500`
- `grid[i][j]` is either `0` or `1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def largestIsland(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])

        # Label each island with an unique index
        idx = 2
        def dfs(i: int, j: int):
            grid[i][j] = idx
            size = 1
            for dx, dy in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                x, y = i + dx, j + dy
                if 0 <= x < m and 0 <= y < n:
                    if grid[x][y] == 1:
                        size += dfs(x, y)
            return size
        
        size_map = {}  # island_idx: island_size

        for i in range(m):
            for j in range(n):
                if grid[i][j] == 1:
                    island_size = dfs(i, j)
                    size_map[idx] = island_size
                    idx += 1

        if not size_map:
            # no island found
            return 1

        max_size = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 0:
                    # get sizes of surrounding islands
                    islands = set()
                    for dx, dy in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                        x, y = i + dx, j + dy
                        if 0 <= x < m and 0 <= y < n and grid[x][y] != 0:
                            islands.add(grid[x][y])
                    sizes = [size_map[island] for island in islands]
                    max_size = max(max_size, sum(sizes) + 1)
        if max_size == 0:
            # no water space
            return m * n
        return max_size
{{< / highlight >}}
</div>
</div>
