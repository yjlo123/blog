---
weight: 11
title: "11 Container With Most Water"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_two_pointers"]
---

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the <code>i<sup>th</sup></code> line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store._

**Notice** that you may not slant the container.

**Example 1:**
<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg" style="width: 100%;"/>
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7].
In this case, the max area of water (blue section) the container can contain is 49.
```
**Example 2:**
```
Input: height = [1,1]
Output: 1
```

**Constraints:**
- `n == height.length`
- <code>2 <= n <= 10<sup>5</sup></code>
- <code>0 <= height[i] <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        max_val = -1
        while l < r:
            max_val = max(max_val, min(height[l], height[r]) * (r-l))
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return max_val
{{< / highlight >}}
</div>
</div>
