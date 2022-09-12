---
weight: 2021
title: "2021 Brightest Position on Street"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array", "lc_prefix_sum"]
---

A perfectly straight street is represented by a number line. The street has street lamp(s) on it and is represented by a 2D integer array `lights`. Each <code>lights[i] = [position<sub>i</sub>, range<sub>i</sub>]</code> indicates that there is a street lamp at position positioni that lights up the area from <code>[position<sub>i</sub> - range<sub>i</sub>, position<sub>i</sub> + range<sub>i</sub>]</code> (**inclusive**).

The **brightness** of a position `p` is defined as the number of street lamp that light up the position `p`.

Given `lights`, return _the **brightest** position on the street. If there are multiple brightest positions, return the **smallest** one._

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2021/09/28/image-20210928155140-1.png" style="width: 100%;"/>
```
Input: lights = [[-3,2],[1,2],[3,3]]
Output: -1
Explanation:
The first street lamp lights up the area from [(-3) - 2, (-3) + 2] = [-5, -1].
The second street lamp lights up the area from [1 - 2, 1 + 2] = [-1, 3].
The third street lamp lights up the area from [3 - 3, 3 + 3] = [0, 6].

Position -1 has a brightness of 2, illuminated by the first and second street light.
Positions 0, 1, 2, and 3 have a brightness of 2,
illuminated by the second and third street light.
Out of all these positions, -1 is the smallest, so return it.
```
**Example 2:**
```
Input: lights = [[1,0],[0,1]]
Output: 1
Explanation:
The first street lamp lights up the area from [1 - 0, 1 + 0] = [1, 1].
The second street lamp lights up the area from [0 - 1, 0 + 1] = [-1, 1].

Position 1 has a brightness of 2, illuminated by the first and second street light.
Return 1 because it is the brightest position on the street.
```
**Example 3:**
```
Input: lights = [[1,2]]
Output: -1
Explanation:
The first street lamp lights up the area from [1 - 2, 1 + 2] = [-1, 3].

Positions -1, 0, 1, 2, and 3 have a brightness of 1,
illuminated by the first street light.
Out of all these positions, -1 is the smallest, so return it.
```

**Constraints:**
- `1 <= lights.length <= 105`
- `lights[i].length == 2`
- <code>-108 <= position<sub>i</sub> <= 108</code>
- <code>0 <= range<sub>i</sub> <= 108</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def brightestPosition(self, lights: List[List[int]]) -> int:
        d = defaultdict(int)
        for light in lights:
            d[light[0] - light[1]] += 1
            d[light[0] + light[1] + 1] -= 1
        max_idx, max_val = -1, -1
        cur = 0
        for k in sorted(d.keys()):
            cur += d[k]
            if cur > max_val:
                max_idx = k
                max_val = cur
        return max_idx
{{< / highlight >}}
</div>
</div>
