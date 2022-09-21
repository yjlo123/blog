---
weight: 723
title: "723 Candy Crush"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_two_pointers"]
---

This question is about implementing a basic elimination algorithm for Candy Crush.

Given an `m x n` integer array `board` representing the grid of candy where `board[i][j]` represents the type of candy. A value of `board[i][j] == 0` represents that the cell is empty.

The given board represents the state of the game following the player's move. Now, you need to restore the board to a stable state by crushing candies according to the following rules:
- If three or more candies of the same type are adjacent vertically or horizontally, crush them all at the same time - these positions become empty.
- After crushing all candies simultaneously, if an empty space on the board has candies on top of itself, then these candies will drop until they hit a candy or bottom at the same time. No new candies will drop outside the top boundary.
- After the above steps, there may exist more candies that can be crushed. If so, you need to repeat the above steps.
- If there does not exist more candies that can be crushed (i.e., the board is stable), then return the current board.

You need to perform the above rules until the board becomes stable, then return _the stable board_.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2018/10/12/candy_crush_example_2.png" style="width: 100%;"/>
```
Input: board = [
    [110,   5, 112, 113, 114],
    [210, 211,   5, 213, 214],
    [310, 311,   3, 313, 314],
    [410, 411, 412,   5, 414],
    [  5,   1, 512,   3,   3],
    [610,   4,   1, 613, 614],
    [710,   1,   2, 713, 714],
    [810,   1,   2,   1,   1],
    [  1,   1,   2,   2,   2],
    [  4,   1,   4,   4,1014]]
Output: [
    [  0,   0,   0,   0,   0],
    [  0,   0,   0,   0,   0],
    [  0,   0,   0,   0,   0],
    [110,   0,   0,   0, 114],
    [210,   0,   0,   0, 214],
    [310,   0,   0, 113, 314],
    [410,   0,   0, 213, 414],
    [610, 211, 112, 313, 614],
    [710, 311, 412, 613, 714],
    [810, 411, 512, 713,1014]]
```
**Example 2:**
```
Input: board = [
    [1,3,5,5,2],
    [3,4,3,3,1],
    [3,2,4,5,2],
    [2,4,4,5,5],
    [1,4,4,1,1]]
Output: [
    [1,3,0,0,0],
    [3,4,0,5,2],
    [3,2,0,3,1],
    [2,4,0,5,2],
    [1,4,3,1,1]]
```

**Constraints:**
- `m == board.length`
- `n == board[i].length`
- `3 <= m, n <= 50`
- `1 <= board[i][j] <= 2000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def candyCrush(self, board: List[List[int]]) -> List[List[int]]:
        m, n = len(board), len(board[0])
        todo = False
        
        # Scan rows
        for i in range(m):
            for j in range(2, n):
                if board[i][j-2] != 0 and abs(board[i][j-2]) == abs(board[i][j-1]) == abs(board[i][j]):
                    board[i][j-2] = board[i][j-1] = board[i][j] = -abs(board[i][j])
                    todo = True
                    
        # Scan columns
        for i in range(2, m):
            for j in range(n):
                if board[i-2][j] != 0 and abs(board[i-2][j]) == abs(board[i-1][j]) == abs(board[i][j]):
                    board[i-2][j] = board[i-1][j] = board[i][j] = -abs(board[i][j])
                    todo = True
        
        # Elimination
        for col in range(n):
            i = j = m - 1
            while j >= 0:
                if board[j][col] > 0:
                    board[i][col] = board[j][col]
                    i -= 1
                j -= 1
            while i >= 0:
                board[i][col] = 0
                i -= 1
        return board if not todo else self.candyCrush(board)
            
{{< / highlight >}}
</div>
</div>
