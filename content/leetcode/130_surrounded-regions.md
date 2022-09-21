---
weight: 130
title: "130 Surrounded Regions"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_dfs"]
---

Given an `m x n` matrix board containing `'X'` and `'O'`, _capture all regions that are 4-directionally surrounded by `'X'`_.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**
```
x X X X    X X X X
X O O X => X X X X
X X O X    X X X X
X O X X    X O X X

Input: board = [
    ["X","X","X","X"],
    ["X","O","O","X"],
    ["X","X","O","X"],
    ["X","O","X","X"]]
Output: [
    ["X","X","X","X"],
    ["X","X","X","X"],
    ["X","X","X","X"],
    ["X","O","X","X"]]
Explanation: Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.
```
**Example 2:**
```
Input: board = [["X"]]
Output: [["X"]]
```

**Constraints:**
- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is `'X'` or `'O'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        m = len(board)
        n = len(board[0])
        def fill(r, c):
            q = deque([(r, c)])
            board[r][c] = '#'
            while q:
                x, y = q.popleft()
                for d in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                    row = x + d[0]
                    col = y + d[1]
                    if (
                        row < 0 or row >= m
                        or col < 0 or col >= n
                        or board[row][col] != 'O'
                    ):
                        continue
                    board[row][col] = '#'
                    q.append((row, col))
        
        for i in range(m):
            for j in [0, n-1]:
                if board[i][j] == 'O':
                    fill(i, j)
        for i in [0, m-1]:
            for j in range(n):
                if board[i][j] == 'O':
                    fill(i, j)
        
        for i in range(m):
            for j in range(n):
                if board[i][j] == '#':
                    board[i][j] = 'O'
                else:
                    board[i][j] = 'X'
{{< / highlight >}}
</div>
</div>
