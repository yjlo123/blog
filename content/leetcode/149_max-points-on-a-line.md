---
weight: 149
title: "149 Max Points on a Line"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_math", "lc_hash_table"]
---

Given an array of `points` where <code>points[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> represents a point on the X-Y plane, return *the maximum number of points that lie on the same straight line*.


**Example 1:**
```
4
3     x
2   x
1 x
0 1 2 3 4 

Input: points = [[1,1],[2,2],[3,3]]
Output: 3
```
**Example 2:**
```
4 x
3   x     x
2     x
1 x     x
0 1 2 3 4 5

Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
```

**Constraints:**
- `1 <= points.length <= 300`
- `points[i].length == 2`
- <code>-10<sup>4</sup> <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>4</sup></code>
- All the `points` are **unique**.

> For a fixed point `points[i]`, consider all other points `points[j]` and calculate the atan2 for each vector `points[j] - points[i]` (the vector with the magnitudes `(points[j].x - points[i].x, points[j].y - points[i].y)`). Then find the maximum number of times some angle value occurs among the calculated values.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxPoints(self, points: List[List[int]]) -> int:
        n = len(points)
        if n == 1:
            return 1
        result = 2
        for i in range(n):
            cnt = collections.defaultdict(int)
            for j in range(n):
                if j != i:
                    cnt[math.atan2(points[j][1] - points[i][1],
                                   points[j][0] - points[i][0])] += 1
            result = max(result, max(cnt.values()) + 1)
        return result
{{< / highlight >}}
</div>
</div>
