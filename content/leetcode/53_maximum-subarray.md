---
weight: 53
title: "53 Maximum Subarray"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array", "lc_dp"]
---

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return _its sum_.

A **subarray** is a **contiguous** part of an array.

**Example 1:**
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
**Example 2:**
```
Input: nums = [1]
Output: 1
```
**Example 3:**
```
Input: nums = [5,4,-1,7,8]
Output: 23
```

**Constraints:**
- 1 <= nums.length <= 3 * 10<sup>4</sup>
- -10<sup>5</sup> <= nums[i] <= 10<sup>5</sup>

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        current_max = all_max = nums[0]
        for n in nums[1:]:
            current_max = max(n, current_max+n)
            all_max = max(all_max, current_max)
        return all_max
{{< / highlight >}}
</div>
</div>
