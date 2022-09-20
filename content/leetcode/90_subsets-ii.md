---
weight: 90
title: "90 Subsets II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_back_tracking"]
---

Given an integer array `nums` that may contain duplicates, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**
```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```
**Example 2:**
```
Input: nums = [0]
Output: [[],[0]]
```

**Constraints:**
- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        if not nums:
            return []
        nums.sort()
        res, cur = [[]], []
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i-1]:
                cur = [item + [nums[i]] for item in cur]
            else:
                cur = [item + [nums[i]] for item in res]
            res += cur
        return res

'''
Backtracking
'''
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []
        track = []
        def backtrack(start):
            res.append(track[:])
            for i in range(start, len(nums)):
                if i > start and nums[i] == nums[i-1]:
                    continue
                track.append(nums[i])
                backtrack(i + 1)
                track.pop()
        backtrack(0)
        return res

{{< / highlight >}}
</div>
</div>
