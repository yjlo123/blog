---
weight: 581
title: "581 Shortest Unsorted Continuous Subarray"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack", "lc_array", "lc_two_pointers"]
---

Given an integer array `nums`, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order.

Return _the shortest such subarray and output its length._

**Example 1:**
```
Input: nums = [2,6,4,8,10,9,15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order
to make the whole array sorted in ascending order.
```
**Example 2:**
```
Input: nums = [1,2,3,4]
Output: 0
```
**Example 3:**
```
Input: nums = [1]
Output: 0
```

**Constraints:**
- <code>1 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        min_val, max_val = float('inf'), float('-inf')
        flag = False
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                flag = True
            if flag:
                min_val = min(min_val, nums[i])
        flag = False
        for i in range(len(nums)-2, -1, -1):
            if nums[i] > nums[i+1]:
                flag = True
            if flag:
                max_val = max(max_val, nums[i])
        
        l, r = 0, len(nums) - 1
        while l < len(nums) and min_val >= nums[l]:
            l += 1
        while r >= 0 and max_val <= nums[r]:
            r -= 1
        return r-l+1 if r-l >= 0 else 0
{{< / highlight >}}
</div>
</div>
