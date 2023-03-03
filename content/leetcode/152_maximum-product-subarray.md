---
weight: 152
title: "152 Maximum Product Subarray"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

Given an integer array `nums`, find a subarray (A **subarray** is a contiguous non-empty sequence of elements within an array.) that has the largest product, and return *the product*.

The test cases are generated so that the answer will fit in a **32-bit** integer.


**Example 1:**
```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
**Example 2:**
```
Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

**Constraints:**
- <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
- `-10 <= nums[i] <= 10`
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

> Record both "max" and "min" up to the number `i` in DP.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        dp_max = [nums[0]]
        dp_min = [nums[0]]
        for i in range(1, len(nums)):
            args = (
                dp_max[-1] * nums[i],
                dp_min[-1] * nums[i],
                nums[i]
            )
            dp_max.append(max(*args))
            dp_min.append(min(*args))
        return max(dp_max)
{{< / highlight >}}
</div>
</div>
