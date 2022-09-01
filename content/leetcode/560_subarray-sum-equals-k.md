---
weight: 560
title: "560 Subarray Sum Equals K"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_hash_table", "lc_array"]
---

Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to `k`._

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**
```
Input: nums = [1,1,1], k = 2
Output: 2
```
**Example 2:**
```
Input: nums = [1,2,3], k = 3
Output: 2
```

**Constraints:**
- <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
- `-1000 <= nums[i] <= 1000`
- <code>-10<sup>7</sup> <= k <= 10<sup>7</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count, s, d = 0, 0, {}
        d[0] = 1
        for num in nums:
            s += num
            if (s - k) in d:
                count += d[s - k]
            d[s] = d.get(s, 0) + 1
        return count
{{< / highlight >}}
</div>
</div>
