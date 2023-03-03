---
weight: 2035
title: "2035 Partition Array Into Two Arrays to Minimize Sum Difference"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_two_pointers", "lc_binary_search", "lc_meet_in_the_middle"]
---

You are given an integer array `nums` of `2 * n` integers. You need to partition `nums` into two arrays of length `n` to **minimize the absolute difference** of the **sums** of the arrays. To partition `nums`, put each element of `nums` into one of the two arrays.

Return *the **minimum** possible absolute difference*.


**Example 1:**
```
arr1: 3  9
nums: 3  9  7  3
arr2:       7  3

Input: nums = [3,9,7,3]
Output: 2
Explanation: One optimal partition is: [3,9] and [7,3].
The absolute difference between the sums of the arrays is abs((3 + 9) - (7 + 3)) = 2.
```
**Example 2:**
```
Input: nums = [-36,36]
Output: 72
Explanation: One optimal partition is: [-36] and [36].
The absolute difference between the sums of the arrays is abs((-36) - (36)) = 72.
```
**Example 3:**
```
arr1: 2         4      -9
nums: 2  -1  0  4  -2  -9
arr2:    -1  0     -2

Input: nums = [2,-1,0,4,-2,-9]
Output: 0
Explanation: One optimal partition is: [2,4,-9] and [-1,0,-2].
The absolute difference between the sums of the arrays is abs((2 + 4 + -9) - (-1 + 0 + -2)) = 0.
```

**Constraints:**
- `1 <= n <= 15`
- `nums.length == 2 * n`
- <code>-10<sup>7</sup> <= nums[i] <= 10<sup>7</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minimumDifference(self, nums: List[int]) -> int:
        h = len(nums) // 2
        left_half, right_half = nums[:h], nums[h:]
        ans = abs(sum(left_half) - sum(right_half))
        total = sum(nums)
        half = total // 2
        
        for k in range(1, h // 2 + 1):
            # select k from left half, and h-k from right half
            left = [sum(comb) for comb in combinations(left_half, k)]
            right = [sum(comb) for comb in combinations(right_half, h - k)]
            right.sort()

            for l in left:
                r = half - l
                p = bisect.bisect_left(right, r) 
                for pp in [p, p - 1]:
                    if 0 <= pp < len(right):
                        left_ans_sum = l + right[pp]
                        right_ans_sum = total - left_ans_sum
                        diff = abs(left_ans_sum - right_ans_sum)
                        ans = min(ans, diff) 
        return ans
{{< / highlight >}}
</div>
</div>
