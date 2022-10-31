---
weight: 79
title: "79 Word Search"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_back_tracking"]
---

Given an `m x n` grid of characters `board` and a string word, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**
```
(A) (B) (C)  E
 S   F  (C)  S
 A  (D) (E)  E

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]],
word = "ABCCED"
Output: true
```
**Example 2:**
```
 A   B   C   E
 S   F   C  (S)
 A   D  (E) (E)

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]],
word = "SEE"
Output: true
```
**Example 3:**
```
 A   B   C   E
 S   F   C   S
 A   D   E   E

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]],
word = "ABCB"
Output: false
```

**Constraints:**
- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger board?

> Try backtracking (DFS) recursively from each cell.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        self.board = board
        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.backtrack(i, j, word):
                    return True
        return False
        
    def backtrack(self, i: int, j: int, suffix: str) -> bool:
        if len(suffix) == 0:
            return True
        
        if (
            i < 0 or i >= len(self.board)
            or j < 0 or j >= len(self.board[0])
            or self.board[i][j] != suffix[0]
        ):
            return False
        
        result = False
        self.board[i][j] = '#'
        for offset in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
            result = self.backtrack(i+offset[0], j+offset[1], suffix[1:])
            if result:
                break # not return here for cleanup side-effects
        self.board[i][j] = suffix[0]
        return result
{{< / highlight >}}
</div>
</div>
