---
weight: 51
title: "51 N-Queens"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_back_tracking"]
---

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**
```
_ Q _ _      _ _ Q _
_ _ _ Q      Q _ _ _
Q _ _ _      _ _ _ Q
_ _ Q _      _ Q _ _

Input: n = 4
Output: [
    [".Q..","...Q","Q...","..Q."],
    ["..Q.","Q...","...Q",".Q.."]
]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above
```
**Example 2:**
```
Input: n = 1
Output: [["Q"]]
```

**Constraints:**
- 1 <= n <= 9

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        def dfs(queens, dif_set, sum_set):
            x = len(queens)
            if x == n:
                result.append(queens)
                return
            for y in range(n):
                # whenever a location (x, y) is occupied, 
                # any other locations (p, q)
                # where p + q == x + y or p - q == x - y 
                # would be invalid.
                if (
                    y not in queens
                    and x-y not in dif_set
                    and x+y not in sum_set
                ): 
                    dfs(
                        queens + [y],
                        dif_set | {x-y},
                        sum_set | {x+y}
                    )  
        result = []
        dfs([], set(), set())
        return [
            ['.'*i + 'Q' + '.'*(n-i-1) for i in sol]
            for sol in result
        ]


'''
Back tracking
'''
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        def backtrack(board, row):
            if row == n:
                res.append([''.join(r) for r in board])
                return
            for col in range(n):
                if not is_valid(board, row, col):
                    continue
                board[row][col] = 'Q'
                backtrack(board, row + 1)
                board[row][col] = '.'
    
        def is_valid(board, row, col):
            # check column
            for i in range(row+1):
                if board[i][col] == 'Q':
                    return False
            i, j = row - 1, col + 1
            # check top-right
            while i >= 0 and j < n:
                if board[i][j] == 'Q':
                    return False
                i -= 1
                j += 1
            i, j = row - 1, col - 1
            # check top-left
            while i >= 0 and j >= 0:
                if board[i][j] == 'Q':
                    return False
                i -= 1
                j -= 1
            return True
        res = []
        board = [['.'] * n for i in range(n)]
        backtrack(board, 0)
        return res
{{< / highlight >}}
</div>
</div>
