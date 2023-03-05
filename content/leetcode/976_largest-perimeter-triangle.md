---
weight: 976
title: "976 Largest Perimeter Triangle"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_greedy"]
---

Given an integer array `nums`, return *the largest perimeter of a triangle with a non-zero area, formed from three of these lengths*. If it is impossible to form any triangle of a non-zero area, return `0`.


**Example 1:**
```
Input: nums = [2,1,2]
Output: 5
Explanation: You can form a triangle with three side lengths: 1, 2, and 2.
```
**Example 2:**
```
Input: nums = [1,2,1,10]
Output: 0
Explanation: 
You cannot use the side lengths 1, 1, and 2 to form a triangle.
You cannot use the side lengths 1, 1, and 10 to form a triangle.
You cannot use the side lengths 1, 2, and 10 to form a triangle.
As we cannot use any three side lengths to form a triangle of non-zero area,
we return 0.
```

**Constraints:**
- <code>3 <= nums.length <= 10<sup>4</sup></code>
- <code>1 <= nums[i] <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def largestPerimeter(self, nums: List[int]) -> int:
        nums.sort()
        for i in range(len(nums)-1, 1, -1):
            if nums[i-1] + nums[i-2] > nums[i]:
                return nums[i] + nums[i-1] + nums[i-2]
        return 0
{{< / highlight >}}
</div>
</div>
