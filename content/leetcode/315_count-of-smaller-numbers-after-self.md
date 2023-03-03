---
weight: 315
title: "315 Count of Smaller Numbers After Self"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_sorting"]
---

Given an integer array `nums`, return *an integer array `counts` where `counts[i]` is the number of smaller elements to the right of `nums[i]`*.


**Example 1:**
```
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```
**Example 2:**
```
Input: nums = [-1]
Output: [0]
```
**Example 3:**
```
Input: nums = [-1,-1]
Output: [0,0]
```

**Constraints:**
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:
        def sort(enums):
            length = len(enums)
            half = length // 2
            if not half:
                return enums
            left, right = sort(enums[:half]), sort(enums[half:])

            # merge in-place
            for i in range(length-1, -1, -1):
                if not right or (left and left[-1][1] > right[-1][1]):
                    # nums remained in right need to shift
                    # to the left of left[-1]
                    res[left[-1][0]] += len(right)
                    enums[i] = left.pop()
                else:
                    enums[i] = right.pop()
            return enums
        res = [0] * len(nums)
        sort(list(enumerate(nums)))
        return res
{{< / highlight >}}
</div>
</div>
