---
weight: 1275
title: "1275 Find Winner on a Tic Tac Toe Game"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_matrix"]
---

**Tic-tac-toe** is played by two players `A` and `B` on a `3 x 3` grid. The rules of Tic-Tac-Toe are:
- Players take turns placing characters into empty squares `' '`.
- The first player `A` always places `'X'` characters, while the second player `B` always places `'O'` characters.
- `'X'` and `'O'` characters are always placed into empty squares, never on filled ones.
- The game ends when there are `three` of the same (non-empty) character filling any row, column, or diagonal.
- The game also ends if all squares are non-empty.
- No more moves can be played if the game is over.

Given a 2D integer array `moves` where moves[i] = [row<sub>i</sub>, col<sub>i</sub>] indicates that the i<sup>th</sup> move will be played on grid[row<sub>i</sub>][col<sub>i</sub>]. return the winner of the game if it exists (`A` or `B`). In case the game ends in a draw return `"Draw"`. If there are still movements to play return `"Pending"`.

You can assume that `moves` is valid (i.e., it follows the rules of **Tic-Tac-Toe**), the grid is initially empty, and `A` will play first.

**Example 1:**
```
x _ _
_ x _
o o x

Input: moves = [[0,0],[2,0],[1,1],[2,1],[2,2]]
Output: "A"
Explanation: A wins, they always play first.
```

**Example 2:**
```
x x o
x o _
o _ _

Input: moves = [[0,0],[1,1],[0,1],[0,2],[1,0],[2,0]]
Output: "B"
Explanation: B wins.
```

**Example 3:**
```
x x o
o o x
x o x

Input: moves = [[0,0],[1,1],[2,0],[1,0],[1,2],[2,1],[0,1],[0,2],[2,2]]
Output: "Draw"
Explanation: The game ends in a draw since there are no moves to make.
```

**Constraints:**
- 1 <= moves.length <= 9
- moves[i].length == 2
- 0 <= row<sub>i</sub>, col<sub>i</sub> <= 2
- There are no repeated elements on `moves`.
- `moves` follow the rules of tic tac toe.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def tictactoe(self, moves: List[List[int]]) -> str:
        n = 3
        rows, cols = [0] * n, [0] * n
        diag = anti_diag = 0
        # A: 1, B: -1
        player = 1
        
        for r, c in moves:
            rows[r] += player
            cols[c] += player
            if r == c:
                diag += player
            if r + c == n - 1:
                anti_diag += player
        
            if any(abs(line) == n for line in (
                rows[r],
                cols[c],
                diag,
                anti_diag,
            )):
                return "A" if player == 1 else "B"
            player *= -1
        return "Draw" if len(moves) == n*n else "Pending"
{{< / highlight >}}
</div>
</div>
