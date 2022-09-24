---
weight: 289
title: "289 Game of Life"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix"]
---

According to Wikipedia's article: "The **Game of Life**, also known simply as **Life**, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

The board is made up of an `m x n` grid of cells, where each cell has an initial state: **live** (represented by a `1`) or **dead** (represented by a `0`). Each cell interacts with its [eight neighbors](https://en.wikipedia.org/wiki/Moore_neighborhood) (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):
1. Any live cell with fewer than two live neighbors dies as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population.
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the `m x n` grid `board`, return _the next state_.

**Example 1:**
```
0 1 0        0 0 0
0 0 1   =>   1 0 1
1 1 1        0 1 1
0 0 0        0 1 0

Input: board = [[0,1,0],[0,0,1],[1,1,1],[0,0,0]]
Output: [[0,0,0],[1,0,1],[0,1,1],[0,1,0]]
```
**Example 2:**
```
1 1  =>  1 1
1 0      1 1

Input: board = [[1,1],[1,0]]
Output: [[1,1],[1,1]]
```

**Constraints:**
- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 25`
- `board[i][j]` is `0` or `1`.

**Follow up:**
- Could you solve it in-place? Remember that the board needs to be updated simultaneously: You cannot update some cells first and then use their updated values to update other cells.
- In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches upon the border of the array (i.e., live cells reach the border). How would you address these problems?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        neighbors = [
            (-1, -1), (-1, 0), (-1, 1),
            (0, -1),           (0, 1),
            (1, -1),  (1, 0),  (1, 1),
        ]
        m = len(board)
        n = len(board[0])
        
        for i in range(m):
            for j in range(n):
                live = 0
                for nei in neighbors:
                    r = i + nei[0]
                    c = j + nei[1]
                    if 0 <= r < m and 0 <= c < n and abs(board[r][c]) == 1:
                        live += 1
                # Rule 1 or 3
                if board[i][j] == 1 and (live < 2 or live > 3):
                    board[i][j] = -1
                # Rule 4
                if board[i][j] == 0 and live == 3:
                    board[i][j] = 2
        for i in range(m):
            for j in range(n):
                board[i][j] = 1 if board[i][j] > 0 else 0
{{< / highlight >}}
</div>
</div>
