---
weight: 695
title: "695 Max Area of Island"
date: 2021-09-23T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_dfs"]
---

You are given an `m x n` binary matrix `grid`. An island is a group of 1's (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value `1` in the island.

_Return the maximum **area** of an island in_ `grid`. If there is no island, return `0`.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg" style="width: 100%;"/>
```
Input: grid = [
    [0,0,1,0,0,0,0,1,0,0,0,0,0],
    [0,0,0,0,0,0,0,1,1,1,0,0,0],
    [0,1,1,0,1,0,0,0,0,0,0,0,0],
    [0,1,0,0,1,1,0,0,1,0,1,0,0],
    [0,1,0,0,1,1,0,0,1,1,1,0,0],
    [0,0,0,0,0,0,0,0,0,0,1,0,0],
    [0,0,0,0,0,0,0,1,1,1,0,0,0],
    [0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The answer is not 11, because the island must be connected 4-directionally.
```

**Example 2:**
```
Input: grid = [[0,0,0,0,0,0,0,0]]
Output: 0
```

**Constraints:**
- m == `grid.length`
- n == `grid[i].length`
- 1 <= m, n <= 50
- `grid[i][j]` is either `0` or `1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        max_area = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1:
                    max_area = max(self.dfs(grid, i, j), max_area)
        return max_area
        
    def dfs(self, grid: List[List[int]], x: int, y: int) -> int:
        count = 0
        stack = [(x, y)]
        while stack:
            i, j = stack.pop()
            if grid[i][j] == 1:
                grid[i][j] = 2
                count += 1
                if i > 0:
                    stack.append((i-1, j))
                if i < len(grid) - 1:
                    stack.append((i+1, j))
                if j > 0:
                    stack.append((i, j-1))
                if j < len(grid[0]) - 1:
                    stack.append((i, j+1))
        return count
{{< / highlight >}}
</div>
</div>
