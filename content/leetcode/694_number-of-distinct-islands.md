---
weight: 694
title: "694 Number of Distinct Islands"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs", "lc_matrix"]
---

You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.

Return _the number of **distinct** islands_.

**Example 1:**
```

Input: grid = [
    [1,1,0,0,0],
    [1,1,0,0,0],
    [0,0,0,1,1],
    [0,0,0,1,1]
]
Output: 1
```
**Example 2:**
```

Input: grid = [
    [1,1,0,1,1],
    [1,0,0,0,0],
    [0,0,0,0,1],
    [1,1,0,1,1]
]
Output: 3
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 50`
- `grid[i][j]` is either `0` or `1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numDistinctIslands(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        island_set = set()
        
        def dfs(x: int, y: int) -> str:
            grid[x][y] = 2
            serialized = ''
            for dx, dy, start, end in [
                ( 1,  0, 'd', 'D'),
                (-1,  0, 'u', 'U'),
                ( 0,  1, 'r', 'R'),
                ( 0, -1, 'l', 'L'),
            ]:
                nx, ny = x + dx, y + dy
                if (
                    0 <= nx < m
                    and 0 <= ny < n
                    and grid[nx][ny] == 1
                ):
                    serialized += (start + dfs(nx, ny) + end)
            return serialized
        
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 1:
                    island = dfs(i, j)
                    island_set.add(island)
        return len(island_set)
{{< / highlight >}}
</div>
</div>
