---
weight: 490
title: "490 The Maze"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs", "lc_matrix"]
---

There is a ball in a `maze` with empty spaces (represented as `0`) and walls (represented as `1`). The ball can go through the empty spaces by rolling **up**, **down**, **left** or **right**, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the `m x n` `maze`, the ball's `start` position and the `destination`, where <code>start = [start<sub>row</sub>, start<sub>col</sub>]</code> and <code>destination = [destination<sub>row</sub>, destination<sub>col</sub>]</code>, return `true` if the ball can stop at the destination, otherwise return `false`.

You may assume that the borders of **the maze are all walls** (see examples).

**Example 1:**
```
# # # # # # #
# _ _ # _ O #
# _ _ _ _ _ #
# _ _ _ # _ #
# # # _ # # #
# _ _ _ _ M #
# # # # # # #

Input: maze = [
    [0,0,1,0,0],
    [0,0,0,0,0],
    [0,0,0,1,0],
    [1,1,0,1,1],
    [0,0,0,0,0]
], start = [0,4], destination = [4,4]
Output: true
Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.
```
**Example 2:**
```
# # # # # # #
# _ _ # _ O #
# _ _ _ _ _ #
# _ _ _ # _ #
# # # M # # #
# _ _ _ _ _ #
# # # # # # #

Input: maze = [
    [0,0,1,0,0],
    [0,0,0,0,0],
    [0,0,0,1,0],
    [1,1,0,1,1],
    [0,0,0,0,0]
], start = [0,4], destination = [3,2]
Output: false
Explanation: There is no way for the ball to stop at the destination. Notice that you can pass through the destination but you cannot stop there.
```
**Example 3:**
```
Input: maze = [
    [0,0,0,0,0],
    [1,1,0,0,1],
    [0,0,0,0,0],
    [0,1,0,0,1],
    [0,1,0,0,0]
], start = [4,3], destination = [0,1]
Output: false
```

**Constraints:**
- `m == maze.length`
- `n == maze[i].length`
- `1 <= m, n <= 100`
- `maze[i][j]` is `0` or `1`.
- `start.length == 2`
- `destination.length == 2`
- <code>0 <= start<sub>row</sub>, destination<sub>row</sub> <= m</code>
- <code>0 <= start<sub>col</sub>, destination<sub>col</sub> <= n</code>
- Both the ball and the destination exist in an empty space, and they will not be in the same position initially.
- The maze contains **at least 2 empty spaces**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def hasPath(self, maze: List[List[int]], start: List[int], destination: List[int]) -> bool:
        m = len(maze)
        n = len(maze[0])
        def dfs(row: int, col: int) -> bool:
            if visited[row][col]:
                return False
            if row == destination[0] and col == destination[1]:
                return True
            visited[row][col] = True
            left, right = col - 1, col + 1
            top, bottom = row - 1, row + 1
            # move right
            while right < n and maze[row][right] == 0:
                right += 1
            if dfs(row, right - 1):
                return True
            # move left
            while left >= 0 and maze[row][left] == 0:
                left -= 1
            if dfs(row, left + 1):
                return True
            # move up
            while top >= 0 and maze[top][col] == 0:
                top -= 1
            if dfs(top + 1, col):
                return True
            # move down
            while bottom < m and maze[bottom][col] == 0:
                bottom += 1
            if dfs(bottom - 1, col):
                return True
            return False
        
        visited = [[False] * n for _ in range(m)]
        return dfs(start[0], start[1])
{{< / highlight >}}
</div>
</div>
