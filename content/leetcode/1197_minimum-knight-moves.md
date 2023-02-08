---
weight: 1197
title: "1197 Minimum Knight Moves"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bfs"]
---

In an infinite chess board with coordinates from `-infinity` to `+infinity`, you have a knight at square `[0, 0]`.

A knight has 8 possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.
```
= - = - = - =
- =[-]=[-]= -
=[-]= - =[-]=
- = - K - = -
=[-]= - =[-]=
- =[-]=[-]= -
= - = - = - =
```
Return *the minimum number of steps needed to move the knight to the square `[x, y]`*. It is guaranteed the answer exists.


**Example 1:**
```
Input: x = 2, y = 1
Output: 1
Explanation: [0, 0] → [2, 1]
```
**Example 2:**
```
Input: x = 5, y = 5
Output: 4
Explanation: [0, 0] → [2, 1] → [4, 2] → [3, 4] → [5, 5]
```

**Constraints:**
- `-300 <= x, y <= 300`
- `0 <= |x| + |y| <= 300`

> Bidirectional BFS

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minKnightMoves(self, x: int, y: int) -> int:
        offsets = [
            (1, 2), (2, 1),
            (2, -1), (1, -2),
            (-1, -2), (-2, -1),
            (-2, 1), (-1, 2)
        ]

        # move from the origin
        q1 = deque([(0, 0, 0)])
        d1 = {(0, 0): 0}

        # move from the target
        q2 = deque([(x, y, 0)])
        d2 = {(x, y): 0}

        while True:
            # check if we reach the circle of target
            x1, y1, s1 = q1.popleft()
            if (x1, y1) in d2:
                return s1 + d2[(x1, y1)]

            # check if we reach the circle of origin
            x2, y2, s2 = q2.popleft()
            if (x2, y2) in d1:
                return s2 + d1[(x2, y2)]

            for ox, oy in offsets:
                # expand the circle of origin
                nx1, ny1 = x1 + ox, y1 + oy
                if (nx1, ny1) not in d1:
                    q1.append((nx1, ny1, s1 + 1))
                    d1[(nx1, ny1)] = s1 + 1

                # expand the circle of target
                nx2, ny2 = x2 + ox, y2 + oy
                if (nx2, ny2) not in d2:
                    q2.append((nx2, ny2, s2 + 1))
                    d2[(nx2, ny2)] = s2 + 1
{{< / highlight >}}
</div>
</div>
