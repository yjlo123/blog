---
weight: 1102
title: "1102 Path With Maximum Minimum Value"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_union_find"]
---

Given an `m x n` integer matrix `grid`, return *the maximum score of a path starting at `(0, 0)` and ending at `(m - 1, n - 1)`* moving in the 4 cardinal directions.

The **score** of a path is the minimum value in that path.
- For example, the score of the path `8 → 4 → 5 → 9` is `4`.

**Example 1:**
```
5 - 4 - 5
        |
1   2   6
        |
7   4   6

Input: grid = [[5,4,5],[1,2,6],[7,4,6]]
Output: 4
Explanation: The path with the maximum score is highlighted in yellow. 
```
**Example 2:**
```
2 - 2   1   2 - 2 - 2
    |       |       |
1   2 - 2 - 2   1   2

Input: grid = [[2,2,1,2,2,2],[1,2,2,2,1,2]]
Output: 2
```
**Example 3:**
```
3 - 4 - 6 - 3 - 4
                |
0   2   1   1   7
                |
8 - 8 - 3   2   7
|       |       |
3   2   4 - 9 - 8
|
4   1   2   0   0
|
4 - 6 - 5 - 4 - 3

Input: grid = [[3,4,6,3,4],[0,2,1,1,7],[8,8,3,2,7],[3,2,4,9,8],[4,1,2,0,0],[4,6,5,4,3]]
Output: 3
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 100`
- <code>0 <= grid[i][j] <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maximumMinimumPath(self, grid: List[List[int]]) -> int:
        def find(x):
            if x != root[x]:
                root[x] = find(root[x])
            return root[x]
        
        def union(x, y):
            root_x = find(x)
            root_y = find(y)
            if root_x != root_y:
                if rank[root_x] > rank[root_y]:
                    root[root_y] = root_x
                elif rank[root_x] < rank[root_y]:
                    root[root_x] = root_y
                else:
                    root[root_y] = root_x
                    rank[root_x] += 1
                
        R = len(grid)
        C = len(grid[0])
        
        dirs = [(1, 0), (0, 1), (-1, 0), (0, -1)]
        rank = [1] * (R * C)
        root = list(range(R * C))
        visited = [[False] * C for _ in range(R)]
        
        # Sort all the cells by values from large to small
        vals = [(row, col) for row in range(R) for col in range(C)]
        vals.sort(key = lambda x: grid[x[0]][x[1]], reverse = True)
        
        for cur_row, cur_col in vals:
            cur_pos = cur_row * C + cur_col
            visited[cur_row][cur_col] = True

            for d_row, d_col in dirs:
                new_row = cur_row + d_row
                new_col = cur_col + d_col
                new_pos = new_row * C + new_col

                # Check if the current cell has any unvisited neighbors with value larger
                # than or equal to val
                if 0 <= new_row < R and 0 <= new_col < C and visited[new_row][new_col]:
                    # If so, we connect the current cell with this neighbor
                    union(cur_pos, new_pos)

            # Check if the top-left cell is connected with the bottom-right cell
            if find(0) == find(R * C - 1):
                return grid[cur_row][cur_col]
        return -1
{{< / highlight >}}
</div>
</div>
