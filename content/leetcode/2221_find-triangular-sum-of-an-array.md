---
weight: 2221
title: "2221 Find Triangular Sum of an Array"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array", "lc_math"]
---

You are given a **0-indexed** integer array `nums`, where `nums[i]` is a digit between `0` and `9` (**inclusive**).

The **triangular sum** of `nums` is the value of the only element present in `nums` after the following process terminates:
1. Let `nums` comprise of n elements. If `n == 1`, end the process. Otherwise, **create** a new **0-indexed** integer array `newNums` of length `n - 1`.
2. For each index i, where `0 <= i < n - 1`, **assign** the value of `newNums[i]` as `(nums[i] + nums[i+1]) % 10`, where `%`denotes modulo operator.
3. **Replace** the array `nums` with `newNums`.
4. **Repeat** the entire process starting from step 1.

Return _the triangular sum of `nums`._

**Example 1:**
```
1   2   3   4   5
 \ / \ / \ / \ /
  3   5   7   9
   \ / \ / \ /
    8   2   6
     \ / \ /
      0   8
       \ /
        8
Input: nums = [1,2,3,4,5]
Output: 8
Explanation:
The above diagram depicts the process from which we obtain the triangular sum of the array.
```
**Example 2:**
```
Input: nums = [5]
Output: 5
Explanation:
Since there is only one element in nums, the triangular sum is the value of that element itself.
```

**Constraints:**
- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 9`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def triangularSum(self, nums: List[int]) -> int:
        n = len(nums)
        while n > 0:
            for i in range(n-1):
                nums[i] = (nums[i] + nums[i+1]) % 10
            n -= 1
        return nums[0]

"""
The nCr can be computed iteratively as
nCr(r + 1) = nCr(r) * (n - r) / (r + 1)
"""
class Solution:
    def triangularSum(self, nums: List[int]) -> int:
        n = len(nums) - 1
        nCr = 1
        res = 0
        for r, num in enumerate(nums):
            res = (res + num  * nCr) % 10
            nCr = nCr * (n - r) // (r + 1)
        return res
{{< / highlight >}}
</div>
</div>
