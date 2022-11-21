---
weight: 413
title: "413 Arithmetic Slices"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp", "lc_math"]
---

An integer array is called arithmetic if it consists of **at least three elements** and if the difference between any two consecutive elements is the same.

- For example, `[1,3,5,7,9]`, `[7,7,7,7]`, and `[3,-1,-5,-9]` are arithmetic sequences.

Given an integer array `nums`, return _the number of arithmetic **subarrays** of `nums`_.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**
```
Input: nums = [1,2,3,4]
Output: 3
Explanation: We have 3 arithmetic slices in nums:
[1, 2, 3], [2, 3, 4] and [1,2,3,4] itself.
```
**Example 2:**
```
Input: nums = [1]
Output: 0
```

**Constraints:**
- `1 <= nums.length <= 5000`
- `-1000 <= nums[i] <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberOfArithmeticSlices(self, nums: List[int]) -> int:
        if len(nums) < 3:
            return 0
        seq = []
        count = 0
        for i in range(2, len(nums)):
            if nums[i] - nums[i-1] == nums[i-1] - nums[i-2]:
                count += 1
            elif count > 0:
                seq.append(count + 2)
                count = 0
        if count > 0:
            seq.append(count + 2)
        res = 0
        for s in seq:
            # 1 + 2 + ... + (n-2) = (1 + (n-2)) * (n-2) / 2
            res += (s*s - s*3 + 2) // 2
        return res


'''
Simplier math solution
'''
class Solution:
    def numberOfArithmeticSlices(self, nums: List[int]) -> int:
        count = 0
        total = 0
        for i in range(2, len(nums)):
            if nums[i] - nums[i-1] == nums[i-1] - nums[i-2]:
                count += 1
            else:
                total += (count + 1) * (count) // 2
                count = 0
        total += count * (count + 1) // 2
        return total


'''
DP:
'''
class Solution:
    def numberOfArithmeticSlices(self, nums: List[int]) -> int:
        dp = 0
        total = 0
        for i in range(2, len(nums)):
            if nums[i] - nums[i-1] == nums[i-1] - nums[i-2]:
                dp += 1
                total += dp
            else:
                dp = 0
        return total
{{< / highlight >}}
</div>
</div>
