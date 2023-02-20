---
weight: 42
title: "42 Trapping Rain Water"
date: 2021-06-26T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_hard", "lc_two_pointers"]
---

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png" style="width: 100%;"/>
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array
[0,1,0,2,1,0,1,3,2,1,2,1].
In this case, 6 units of rain water (blue section) are being trapped.
```


**Example 2:**
```
Input: height = [4,2,0,3,2,5]
Output: 9
```

**Constraints:**

- `n == height.length`
- <code>0 <= n <= 3 * 10<sup>4</sup></code>
- <code>0 <= height[i] <= 10<sup>5</sup></code>

> Two pointers from both sides, and record the max from both sides

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def trap(self, height: List[int]) -> int:
        res = 0
        l, r = 0, len(height) - 1
        max_l, max_r = -1, -1
        while l <= r:
            if height[l] <= height[r]:
                if height[l] > max_l:
                    max_l = height[l]
                else:
                    res += max_l - height[l]
                l += 1
            else:
                if height[r] > max_r:
                    max_r = height[r]
                else:
                    res += max_r - height[r]
                r -= 1
        return res
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func trap(height []int) int {
    n := len(height)
    left := 0
    right := n - 1
    res := 0
    maxLeft := 0
    maxRight := 0

    for left <= right {
        if height[left] <= height[right] {
            if height[left] > maxLeft {
                maxLeft = height[left]
            } else {
                res += maxLeft - height[left]
            }
            left++
        } else {
            if height[right] >= maxRight {
                maxRight = height[right]
            } else {
                res += maxRight - height[right]
            }
            right--
        }
    }
    return res
}
{{< / highlight >}}
</div>
</div>
