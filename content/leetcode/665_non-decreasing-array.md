---
weight: 665
title: "665 Non-decreasing Array"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array"]
---

Given an array `nums` with `n` integers, your task is to check if it could become non-decreasing by modifying **at most one element**.

We define an array is non-decreasing if `nums[i] <= nums[i + 1]` holds for every i (**0-based**) such that (`0 <= i <= n - 2`).

**Example 1:**
```
Input: nums = [4,2,3]
Output: true
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
```
**Example 2:**
```
Input: nums = [4,2,1]
Output: false
Explanation: You cannot get a non-decreasing array by modifying at most one element.
```

**Constraints:**
- `n == nums.length`
- <code>1 <= n <= 10<sup>4</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def checkPossibility(self, nums: List[int]) -> bool:
        p = -1
        for i in range(len(nums) - 1):
            if nums[i+1] < nums[i]:
                if p >= 0:
                    return False
                p = i
        return (
            p == -1 or p == 0 or p == len(nums)-2
            or nums[p-1] <= nums[p+1]
            or nums[p] <= nums[p+2]
        )
{{< / highlight >}}
</div>
</div>
