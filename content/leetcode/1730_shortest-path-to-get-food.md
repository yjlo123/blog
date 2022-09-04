---
weight: 1730
title: "1730 Shortest Path to Get Food"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bfs", "lc_matrix"]
---

You are starving and you want to eat food as quickly as possible. You want to find the shortest path to arrive at any food cell.

You are given an `m x n` character matrix, `grid`, of these different types of cells:
- `'*'` is your location. There is **exactly one** '*' cell.
- `'#'` is a food cell. There may be **multiple** food cells.
- `'O'` is free space, and you can travel through these cells.
- `'X'` is an obstacle, and you cannot travel through these cells.

You can travel to any adjacent cell north, east, south, or west of your current location if there is not an obstacle.

Return _the **length** of the shortest path for you to reach **any** food cell._ If there is no path for you to reach food, return `-1`.

**Example 1:**
```

Input: grid = [
["X","X","X","X","X","X"],
["X","*","O","O","O","X"],
["X","O","O","#","O","X"],
["X","X","X","X","X","X"]]
Output: 3
Explanation: It takes 3 steps to reach the food.
```
**Example 2:**
```
Input: grid = [
["X","X","X","X","X"],
["X","*","X","O","X"],
["X","O","X","#","X"],
["X","X","X","X","X"]]
Output: -1
Explanation: It is not possible to reach the food.
```
**Example 3:**
```
Input: grid = [
["X","X","X","X","X","X","X","X"],
["X","*","O","X","O","#","O","X"],
["X","O","O","X","O","O","X","X"],
["X","O","O","O","O","#","O","X"],
["X","X","X","X","X","X","X","X"]]
Output: 6
Explanation: There can be multiple food cells.
It only takes 6 steps to reach the bottom food.
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 200`
- `grid[row][col]` is `'*'`, `'X'`, `'O'`, or` '#'`.
- The grid contains **exactly one** `'*'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    def getFood(self, grid: List[List[str]]) -> int:
        m, n = len(grid), len(grid[0])
        start = (-1, -1)
        q = deque()
        for r in range(m):
            for c in range(n):
                if grid[r][c] == '*':
                    q.append((r, c))
                    break
        dis = 0
        while q:
            dis += 1
            q_size = len(q)
            for i in range(q_size):
                cell = q.popleft()
                for d in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                    x = cell[0] + d[0]
                    y = cell[1] + d[1]
                    if x < 0 or y < 0 or x >= m or y >= n:
                        continue
                    if grid[x][y] == '#':
                        return dis
                    if grid[x][y] == 'O':
                        q.append((x, y))
                        grid[x][y] = 'v'
        return -1
{{< / highlight >}}
</div>
</div>
