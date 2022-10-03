---
weight: 1099
title: "1099 Two Sum Less Than K"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_two_pointers"]
---

Given an array `nums` of integers and integer `k`, return the maximum sum such that there exists `i < j` with `nums[i] + nums[j] = sum` and `sum < k`. If no `i`, `j` exist satisfying this equation, return `-1`.

**Example 1:**
```
Input: nums = [34,23,1,24,75,33,54,8], k = 60
Output: 58
Explanation: We can use 34 and 24 to sum 58 which is less than 60.
```
**Example 2:**
```
Input: nums = [10,20,30], k = 15
Output: -1
Explanation: In this case it is not possible to get a pair sum less that 15.
```

**Constraints:**
- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 1000`
- `1 <= k <= 2000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def twoSumLessThanK(self, nums: List[int], k: int) -> int:
        nums.sort()
        max_sum = -1
        l , r = 0, len(nums) - 1
        while l < r:
            if nums[l] + nums[r] >= k:
                r -= 1
            else:
                max_sum = max(max_sum, nums[l] + nums[r])
                l += 1
        return max_sum
{{< / highlight >}}
</div>
</div>
