---
weight: 36
title: "36 Valid Sudoku"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_hash_table"]
---

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

Each row must contain the digits `1-9` without repetition.
Each column must contain the digits `1-9` without repetition.
Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**
- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

**Example 1:**
```
5 3 _ | _ 7 _ | _ _ _
6 _ _ | 1 9 5 | _ _ _
_ 9 8 | _ _ _ | _ 6 _
---------------------
8 _ _ | _ 6 _ | _ _ 3
4 _ _ | 8 _ 3 | _ _ 1
7 _ _ | _ 2 _ | _ _ 6
---------------------
_ 6 _ | _ _ _ | 2 8 _
_ _ _ | 4 1 9 | _ _ 5
_ _ _ | _ 8 _ | _ 7 9

Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```
**Example 2:**
```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8.
Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Constraints:**
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        def check_duplicates(lst):
            clean_r = [c for c in lst if c != '.']
            if len(clean_r) != len(set(clean_r)):
                return False
            return True
            
        # check rows
        for r in board:
            if not check_duplicates(r):
                return False
        
        # check columns
        for i in range(9):
            column = [r[i] for r in board]
            if not check_duplicates(column):
                return False
        
        # check sub-boxes
        for i in range(3):
            for j in range(3):
                sub = []
                for k in range(3):
                    sub.extend(board[i*3+k][j*3:j*3+3])
                if not check_duplicates(sub):
                    return False
        return True
{{< / highlight >}}
</div>
</div>
