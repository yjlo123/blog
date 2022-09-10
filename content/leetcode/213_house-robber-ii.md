---
weight: 213
title: "213 House Robber II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**._

**Example 1:**
```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
because they are adjacent houses.
```
**Example 2:**
```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```
**Example 3:**
```
Input: nums = [1,2,3]
Output: 3
```

**Constraints:**
- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 3:
            return max(nums)
        return max(
            self.rob_simple(nums[:-1]),
            self.rob_simple(nums[1:])
        )

    def rob_simple(self, nums: List[int]) -> int:
        t1 = t2 = 0
        for current in nums:
            t1, t2 = max(t1, current + t2), t1
        return t1
{{< / highlight >}}
</div>
</div>
