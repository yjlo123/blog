---
weight: 611
title: "611 Valid Triangle Number"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array", "lc_two_pointers"]
---

Given an integer array `nums`, return _the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle_.

**Example 1:**
```
Input: nums = [2,2,3,4]
Output: 3
Explanation: Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```
**Example 2:**
```
Input: nums = [4,2,3,4]
Output: 4
```

**Constraints:**
- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()
        ans = 0
        n = len(nums)
        
        # c < (a + b)
        for i in range(n-1, 1, -1):
            l, r = 0, i - 1
            while l < r:
                if nums[i] < nums[l] + nums[r]:
                    ans += r - l
                    r -= 1
                else:
                    l += 1
        return ans
{{< / highlight >}}
</div>
</div>
