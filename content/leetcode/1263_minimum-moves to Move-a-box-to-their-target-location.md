---
weight: 1263
title: "1263 Minimum Moves to Move a Box to Their Target Location"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs"]
---

A storekeeper is a game in which the player pushes boxes around in a warehouse trying to get them to target locations.

The game is represented by an `m x n` grid of characters `grid` where each element is a wall, floor, or box.

Your task is to move the box `'B'` to the target position `'T'` under the following rules:

- The character `'S'` represents the player. The player can move up, down, left, right in `grid` if it is a floor (empty cell).
- The character `'.'` represents the floor which means a free cell to walk.
- The character `'#'` represents the wall which means an obstacle (impossible to walk there).
- There is only one box `'B'` and one target cell `'T'` in the `grid`.
- The box can be moved to an adjacent free cell by standing next to the box and then moving in the direction of the box. This is a **push**.
- The player cannot walk through the box.

Return *the minimum number of **pushes** to move the box to the target*. If there is no way to reach the target, return `-1`.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2019/11/06/sample_1_1620.png" style="width: 100%;"/>
```
Input: grid = [["#","#","#","#","#","#"],
               ["#","T","#","#","#","#"],
               ["#",".",".","B",".","#"],
               ["#",".","#","#",".","#"],
               ["#",".",".",".","S","#"],
               ["#","#","#","#","#","#"]]
Output: 3
Explanation: We return only the number of times the box is pushed.
```
**Example 2:**
```
Input: grid = [["#","#","#","#","#","#"],
               ["#","T","#","#","#","#"],
               ["#",".",".","B",".","#"],
               ["#","#","#","#",".","#"],
               ["#",".",".",".","S","#"],
               ["#","#","#","#","#","#"]]
Output: -1
```
**Example 3:**
```
Input: grid = [["#","#","#","#","#","#"],
               ["#","T",".",".","#","#"],
               ["#",".","#","B",".","#"],
               ["#",".",".",".",".","#"],
               ["#",".",".",".","S","#"],
               ["#","#","#","#","#","#"]]
Output: 5
Explanation: push the box down, left, left, up and up.
```

**Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 20`
- `grid` contains only characters `'.'`, `'#'`, `'S'`, `'T'`, or `'B'`.
- There is only one character `'S'`, `'B'`, and `'T'` in the `grid`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minPushBox(self, grid: List[List[str]]) -> int:
        m, n = len(grid), len(grid[0])
        target = init_box = init_person = (0, 0)
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 'T':
                    target = (i, j)
                if grid[i][j] == 'B':
                    init_box = (i, j)
                if grid[i][j] == 'S':
                    init_person = (i, j)
        
        def valid(pos: Tuple[int, int]):
            x, y = pos
            return (
                0 <= x < m and
                0 <= y < n and
                grid[x][y] != '#'
            )
        
        def can_reach(curr, dest, box):
            # dfs
            q = deque([curr])
            visited = set([curr])
            while q:
                pos = q.popleft()
                if pos == dest:
                    return True
                for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                    next_pos = pos[0] + dx, pos[1] + dy
                    if (valid(next_pos) and
                        next_pos not in visited and
                        next_pos != box
                    ):
                        visited.add(next_pos)
                        q.append(next_pos)
            return False
        
        q = deque()
        q.append((0, init_box, init_person))
        seen = set()  # records of (box_pos, per_pos) after push

        while q:
            dist, box, person = q.popleft()
            if box == target:
                return dist
            bx, by = box
            moves = [
                # 4 cases for
                # (box pos after push + person position before push)
                ((bx+1, by), (bx-1, by)),
                ((bx-1, by), (bx+1, by)),
                ((bx, by+1), (bx, by-1)),
                ((bx, by-1), (bx, by+1)),
            ]
            for box_new, per_before in moves:
                # per_before -> box -> box_new
                # per_before is the person position beofre push
                # box is the new person position after push
                if (valid(box_new) and
                    (box_new, box) not in seen and
                    valid(per_before) and
                    can_reach(person, per_before, box)
                ):
                    seen.add((box_new, box))
                    q.append((dist + 1, box_new, box))
        return -1
{{< / highlight >}}
</div>
</div>
