---
weight: 2345
title: "2345 Finding the Number of Visible Mountains"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack"]
---

You are given a **0-indexed** 2D integer array `peaks` where <code>peaks[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> states that mountain `i` has a peak at coordinates <code>(x<sub>i</sub>, y<sub>i</sub>)</code>. A mountain can be described as a right-angled isosceles triangle, with its base along the `x`-axis and a right angle at its peak. More formally, the **gradients** of ascending and descending the mountain are `1` and `-1` respectively.

A mountain is considered **visible** if its peak does not lie within another mountain (including the border of other mountains).

Return _the number of visible mountains_.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2022/07/19/ex1.png" style="width: 60%;"/>
```
Input: peaks = [[2,2],[6,3],[5,4]]
Output: 2
Explanation: The diagram above shows the mountains.
- Mountain 0 is visible since its peak does not lie within another mountain or its sides.
- Mountain 1 is not visible since its peak lies within the side of mountain 2.
- Mountain 2 is visible since its peak does not lie within another mountain or its sides.
There are 2 mountains that are visible.
```
**Example 2:**
<img src="https://assets.leetcode.com/uploads/2022/07/19/ex2new1.png" style="width: 60%;"/>
```
Input: peaks = [[1,3],[1,3]]
Output: 0
Explanation: The diagram above shows the mountains (they completely overlap).
Both mountains are not visible since their peaks lie within each other.
```

**Constraints:**
- <code>1 <= peaks.length <= 10<sup>5</sup></code>
- `peaks[i].length == 2`
- <code>1 <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def visibleMountains(self, peaks: List[List[int]]) -> int:
        stack = []
        cur_max = 0
        for x, y in sorted(peaks):
            # find slope
            left, right = x - y, x + y 
            
            # remove left mountains that got overlapped
            while stack and stack[-1] >= left:
                stack.pop()
            
            # skip right mountains overlapped by the current
            if right > cur_max: 
                cur_max = right 
                stack.append(left)
        return len(stack)
{{< / highlight >}}
</div>
</div>
