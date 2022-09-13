---
weight: 909
title: "909 Snakes and Ladders"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_bfs"]
---

You are given an `n x n` integer matrix `board` where the cells are labeled from `1` to <code>n<sup>2</sup></code> in a [Boustrophedon style](https://en.wikipedia.org/wiki/Boustrophedon) starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square `1` of the board. In each move, starting from square `curr`, do the following:
- Choose a destination square `next` with a label in the range <code>[curr + 1, min(curr + 6, n<sup>2</sup>)]</code>.
  - This choice simulates the result of a standard **6-sided die roll**: i.e., there are always at most 6 destinations, regardless of the size of the board.
- If `next` has a snake or ladder, you must move to the destination of that snake or ladder. Otherwise, you move to `next`.
- The game ends when you reach the square <code>n<sup>2</sup></code>.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares `1` and <code>n<sup>2</sup></code> do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do **not** follow the subsequent snake or ladder.
- For example, suppose the board is `[[-1,4],[-1,3]]`, and on the first move, your destination square is `2`. You follow the ladder to square 3, but do **not** follow the subsequent ladder to `4`.

Return _the least number of moves required to reach the square <code>n<sup>2</sup></code>. If it is not possible to reach the square, return `-1`_.

**Example 1:**
<div style="text-align:center;"><img src="https://assets.leetcode.com/uploads/2018/09/23/snakes.png" style="width: 60%; margin: auto;"/></div>

```
Input: board = [
    [-1,-1,-1,-1,-1,-1],
    [-1,-1,-1,-1,-1,-1],
    [-1,-1,-1,-1,-1,-1],
    [-1,35,-1,-1,13,-1],
    [-1,-1,-1,-1,-1,-1],
    [-1,15,-1,-1,-1,-1]
]
Output: 4
Explanation: 
In the beginning, you start at square 1 (at row 5, column 0).
You decide to move to square 2 and must take the ladder to square 15.
You then decide to move to square 17 and must take the snake to square 13.
You then decide to move to square 14 and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
This is the lowest possible number of moves to reach the last square, so return 4.
```
**Example 2:**
```
Input: board = [[-1,-1],[-1,3]]
Output: 1
```

**Constraints:**
- `n == board.length == board[i].length`
- `2 <= n <= 20`
- `grid[i][j]` is either `-1` or in the range <code>[1, n<sup>2</sup>]</code>.
- The squares labeled `1` and <code>n<sup>2</sup></code> do not have any ladders or snakes.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def snakesAndLadders(self, board: List[List[int]]) -> int:
        n = len(board)
        need = {1: 0}
        bfs = [1]
        for x in bfs:
            for i in range(x + 1, x + 7):
                a, b = (i - 1) // n, (i - 1) % n
                # ~i: index from bottom or right
                nxt = board[~a][b if a % 2 == 0 else ~b]
                if nxt > 0:
                    i = nxt
                if i == n * n:
                    # on last cell
                    return need[x] + 1
                if i not in need:
                    need[i] = need[x] + 1
                    bfs.append(i)
        return -1
{{< / highlight >}}
</div>
</div>
