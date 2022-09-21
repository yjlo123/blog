---
weight: 286
title: "286 Walls and Gates"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs", "lc_matrix"]
---

You are given an `m x n` grid `rooms` initialized with these three possible values.

- `-1` A wall or an obstacle.
- `0` A gate.
- `INF` Infinity means an empty room. We use the value <code>2<sup>31</sup> - 1 = 2147483647</code> to represent `INF` as you may assume that the distance to a gate is less than `2147483647`.

Fill each empty room with the distance to _its nearest gate_. If it is impossible to reach a gate, it should be filled with `INF`.

**Example 1:**
```
_ # G _   3 # 0 1
_ _ _ #   2 2 1 #
_ # _ #   1 # 2 #
G # _ _   0 # 3 $

Input: rooms = [
    [2147483647,-1,0,2147483647],
    [2147483647,2147483647,2147483647,-1],
    [2147483647,-1,2147483647,-1],
    [0,-1,2147483647,2147483647]
]
Output: [[3,-1,0,1],[2,2,1,-1],[1,-1,2,-1],[0,-1,3,4]]
```
**Example 2:**
```
Input: rooms = [[-1]]
Output: [[-1]]
```

**Constraints:**
- `m == rooms.length`
- `n == rooms[i].length`
- `1 <= m, n <= 250`
- `rooms[i][j]` is `-1`, `0`, or <code>2<sup>31</sup> - 1</code>.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    INF = 2147483647
    
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        m = len(rooms)
        n = len(rooms[0])
        q = deque()
        for i in range(m):
            for j in range(n):
                if rooms[i][j] == 0:
                    q.append((i, j))
        '''
        Each gate only looks at the areas within 1 space before
        we check the next gate. So each area within one space of
        the gates are checked for rooms and these rooms are marked,
        then added to the queue. Once all gates are checked, each
        new space is checked, and so forth. So, once a room gets
        hit, it has to be from the closest gate.
        '''
        while q:
            x, y = q.popleft()
            for d in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                r = x + d[0]
                c = y + d[1]
                if (
                    r < 0 or r >= m
                    or c < 0 or c >= n
                    or rooms[r][c] != self.INF
                ):
                    continue
                q.append((r, c))
                rooms[r][c] = rooms[x][y] + 1
{{< / highlight >}}
</div>
</div>
