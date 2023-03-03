---
weight: 1755
title: "1755 Closest Subsequence Sum"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_two_pointers", "lc_meet_in_the_middle"]
---

You are given an integer array `nums` and an integer `goal`.

You want to choose a subsequence of `nums` such that the sum of its elements is the closest possible to `goal`. That is, if the sum of the subsequence's elements is `sum`, then you want to minimize the absolute difference `abs(sum - goal)`.

Return *the **minimum** possible value of `abs(sum - goal)`*.

Note that a subsequence of an array is an array formed by removing some elements **(possibly all or none)** of the original array.


**Example 1:**
```
Input: nums = [5,-7,3,5], goal = 6
Output: 0
Explanation: Choose the whole array as a subsequence, with a sum of 6.
This is equal to the goal, so the absolute difference is 0.
```
**Example 2:**
```
Input: nums = [7,-9,15,-2], goal = -5
Output: 1
Explanation: Choose the subsequence [7,-9,-2], with a sum of -4.
The absolute difference is abs(-4 - (-5)) = abs(1) = 1, which is the minimum.
```
**Example 3:**
```
Input: nums = [1,2,3], goal = -7
Output: 7
```

**Constraints:**
- `1 <= nums.length <= 40`
- <code>-10<sup>7</sup> <= nums[i] <= 10<sup>7</sup></code>
- <code>-10<sup>9</sup> <= goal <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minAbsDifference(self, nums: List[int], goal: int) -> int:
        n = len(nums)

        # all possible sums of given array
        def get_all_sums(arr):
            sums = {0}            
            for a in arr:
                sums |= {s + a for s in sums}
            return sums 
        
        s1 = sorted(get_all_sums(nums[:n//2]))
        s2 = sorted(get_all_sums(nums[n//2:]))

        best = math.inf
        l = 0
        r = len(s2) - 1
        # find the sum of two sums from s1 and s2 respectively
        # that gives a value closest to the goal
        while l < len(s1) and r >= 0:
            s = s1[l] + s2[r]
            best = min(best, abs(s - goal))
            if s == goal:
                return 0
            elif s < goal:
                l += 1
            else:
                r -= 1
        return best
{{< / highlight >}}
</div>
</div>
