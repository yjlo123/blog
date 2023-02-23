---
weight: 1610
title: "1610 Maximum Number of Visible Points"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_sliding_window"]
---

You are given an array `points`, an integer `angle`, and your `location`, where <code>location = [pos<sub>x</sub>, pos<sub>y</sub>]</code> and <code>points[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> both denote **integral coordinates** on the X-Y plane.

Initially, you are facing directly east from your position. You **cannot move** from your position, but you can **rotate**. In other words, <code>pos<sub>x</sub></code> and <code>pos<sub>y</sub></code> cannot be changed. Your field of view in **degrees** is represented by `angle`, determining how wide you can see from any given view direction. Let `d` be the amount in degrees that you rotate counterclockwise. Then, your field of view is the **inclusive** range of angles `[d - angle/2, d + angle/2]`.

<video width="480" height="360" controls>
  <source src="https://assets.leetcode.com/uploads/2020/09/30/angle.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

You can **see** some set of points if, for each point, the **angle** formed by the point, your position, and the immediate east direction from your position is **in your field of view**.

There can be multiple points at one coordinate. There may be points at your location, and you can always see these points regardless of your rotation. Points do not obstruct your vision to other points.

Return _the maximum number of points you can see_.

**Example 1:**
```
4
3     *
2   *
1 x *
0 1 2 3 4

Input: points = [[2,1],[2,2],[3,3]], angle = 90, location = [1,1]
Output: 3
Explanation: The shaded region represents your field of view.
All points can be made visible in your field of view, including [3,3]
even though [2,2] is in front and in the same line of sight.
```
**Example 2:**
```
Input: points = [[2,1],[2,2],[3,4],[1,1]], angle = 90, location = [1,1]
Output: 4
Explanation: All points can be made visible in your field of view,
including the one at your location.
```
**Example 3:**
```
3
2
1 x *
0 * 2 3 4

Input: points = [[1,0],[2,1]], angle = 13, location = [1,1]
Output: 1
Explanation: You can only see one of the two points, as shown above.
```

**Constraints:**
- <code>1 <= points.length <= 10<sup>5</sup></code>
- `points[i].length == 2`
- `location.length == 2`
- `0 <= angle < 360`
- <code>0 <= pos<sub>x</sub>, posy, x<sub>i</sub>, y<sub>i</sub> <= 100</code>

> `math.atan2(y, x)` returns value of `atan(y/x)` in radians. The `atan2()` method returns a numeric value between `-𝝿` and `𝝿` representing the angle θ of a `(x, y)` point and positive x-axis.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def visiblePoints(
        self,
        points: List[List[int]],
        angle: int,
        location: List[int]
    ) -> int:
        point_angles = []
        on_viewer = 0 # num of points on the viewer location

        for p in points:
            if p == location:
                on_viewer += 1
                continue
            radian = math.atan2(p[1]-location[1], p[0]-location[0])
            degree = math.degrees(radian)
            if degree < 0:
                degree += 360
            point_angles.append(degree)
        
        point_angles.sort()
        point_angles += [a + 360 for a in point_angles]

        max_count = 0
        lo = 0
        for hi in range(len(point_angles)):
            while point_angles[hi] - point_angles[lo] > angle:
                lo += 1
            max_count = max(max_count, hi - lo + 1)

        return max_count + on_viewer
{{< / highlight >}}
</div>
</div>
