---
weight: 419
title: "419 Battleships in a Board"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs", "lc_matrix"]
---

Given an `m x n` matrix board where each cell is a battleship `'X'` or empty `'.'`, return *the number of the **battleships** on `board`*.

**Battleships** can only be placed horizontally or vertically on `board`. In other words, they can only be made of the shape `1 x k` (`1` row, `k` columns) or `k x 1` (`k` rows, `1` column), where `k` can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).


**Example 1:**
```
X _ _ X
_ _ _ X
_ _ _ X
_ _ _ _

Input: board = [["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]
Output: 2
```
**Example 2:**
```
Input: board = [["."]]
Output: 0
```

**Constraints:**
- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is either `'.'` or `'X'`.

**Follow up:** Could you do it in one-pass, using only `O(1)` extra memory and without modifying the values `board`?

> Find all the top-left corners of the ships

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def countBattleships(self, board: List[List[str]]) -> int:
        m, n = len(board), len(board[0])
        count = 0
        for i in range(m):
            for j in range(n):
                if (
                    board[i][j] == 'X' and
                    (i == 0 or board[i-1][j] != 'X') and
                    (j == 0 or board[i][j-1] != 'X')
                ):
                    count += 1
        return count
{{< / highlight >}}
</div>
</div>
