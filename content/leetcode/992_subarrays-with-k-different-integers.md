---
weight: 992
title: "992 Subarrays with K Different Integers"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_sliding_window"]
---

Given an integer array `nums` and an integer `k`, return _the number of **good subarrays** of `nums`_.

A **good array** is an array where the number of different integers in that array is exactly `k`.

- For example, `[1,2,3,1,2]` has `3` different integers: `1`, `2`, and `3`.
A **subarray** is a **contiguous** part of an array.


**Example 1:**
```
Input: nums = [1,2,1,2,3], k = 2
Output: 7
Explanation: Subarrays formed with exactly 2 different integers:
[1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2]
```
**Example 2:**
```
Input: nums = [1,2,1,3,4], k = 3
Output: 3
Explanation: Subarrays formed with exactly 3 different integers:
[1,2,1,3], [2,1,3], [1,3,4].
```

**Constraints:**
- <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
- `1 <= nums[i], k <= nums.length`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        n = len(nums)
        
        def at_most_k(k):
            count = collections.defaultdict(int)
            res, i = 0, 0
            for j in range(n):
                # move window right
                if count[nums[j]] == 0:
                    k -= 1
                count[nums[j]] += 1
                while k < 0:
                    # move window left
                    count[nums[i]] -= 1
                    if count[nums[i]] == 0:
                        k += 1
                    i += 1
                # add windows size (with at most k distinct)
                res += j - i + 1
            return res

        return at_most_k(k) - at_most_k(k-1)
{{< / highlight >}}
</div>
</div>
