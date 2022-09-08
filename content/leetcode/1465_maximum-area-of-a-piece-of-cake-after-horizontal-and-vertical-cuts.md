---
weight: 1465
title: "1465 Maximum Area of a Piece of Cake After Horizontal and Vertical Cuts"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_greedy"]
---

You are given a rectangular cake of size `h x w` and two arrays of integers `horizontalCuts` and `verticalCuts` where:
- `horizontalCuts[i]` is the distance from the top of the rectangular cake to the <code>i<sup>th</sup></code> horizontal cut and similarly, and
- `verticalCuts[j]` is the distance from the left of the rectangular cake to the <code>j<sup>th</sup></code> vertical cut.

Return _the maximum area of a piece of cake after you cut at each horizontal and vertical position provided in the arrays `horizontalCuts` and `verticalCuts`_. Since the answer can be a large number, return this modulo <code>10<sup>9</sup> + 7</code>.

**Example 1:**
```
 0  1  2  3  4
0   |     |
1---|-----|---
2---|-----|---
3   |     |
4---|-----|---
5   |     |

Input: h = 5, w = 4, horizontalCuts = [1,2,4], verticalCuts = [1,3]
Output: 4 
Explanation: The figure above represents the given rectangular cake. Red lines are the horizontal and vertical cuts. After you cut the cake, the green piece of cake has the maximum area.
```
**Example 2:**
```
 0  1  2  3  4
0   |
1---|---------
2   |
3---|---------
4   |
5   |

Input: h = 5, w = 4, horizontalCuts = [3,1], verticalCuts = [1]
Output: 6
Explanation: The figure above represents the given rectangular cake. Red lines are the horizontal and vertical cuts. After you cut the cake, the green and yellow pieces of cake have the maximum area.
Example 3:

Input: h = 5, w = 4, horizontalCuts = [3], verticalCuts = [3]
Output: 9
```

**Constraints:**
- <code>2 <= h, w <= 10<sup>9</sup></code>
- <code>1 <= horizontalCuts.length <= min(h - 1, 10<sup>5</sup>)</code>
- <code>1 <= verticalCuts.length <= min(w - 1, 10<sup>5</sup>)</code>
- `1 <= horizontalCuts[i] < h`
- `1 <= verticalCuts[i] < w`
- All the elements in `horizontalCuts` are distinct.
- All the elements in `verticalCuts` are distinct.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxArea(
        self,
        h: int,
        w: int,
        horizontalCuts: List[int],
        verticalCuts: List[int]
    ) -> int:
        MOD = 10 ** 9 + 7
        hor = [0] + sorted(horizontalCuts) + [h]
        ver = [0] + sorted(verticalCuts) + [w]
        max_h, max_v = -1, -1
        for i in range(1, len(hor)):
            max_h = max(max_h, hor[i] - hor[i-1])
        for i in range(1, len(ver)):
            max_v = max(max_v, ver[i] - ver[i-1])
        return (max_h * max_v) % MOD
{{< / highlight >}}
</div>
</div>
