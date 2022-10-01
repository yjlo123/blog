---
weight: 46
title: "46 Permutations"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_back_tracking"]
---

Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in any order.

**Example 1:**
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```
**Example 2:**
```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```
**Example 3:**
```
Input: nums = [1]
Output: [[1]]
```

**Constraints:**
- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are unique.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:

    def permute(self, nums: List[int]) -> List[List[int]]:
        if not nums:
            return [[]]
        res = []
        for i, num in enumerate(nums):
            perm = self.permute(nums[:i] + nums[i+1:])
            for p in perm:
                res.append([num] + p)
        return res
{{< / highlight >}}
</div>
</div>
