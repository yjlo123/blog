---
weight: 1413
title: "1413 Minimum Value to Get Positive Step by Step Sum"
date: 2021-03-28T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

Given an array of integers nums, you start with an initial **positive** value startValue.

In each iteration, you calculate the step by step sum of _startValue_ plus elements in `nums` (from left to right).

Return the minimum **positive** value of _startValue_ such that the step by step sum is never less than 1.

**Example 1:**
```
Input: nums = [-3,2,-3,4,2]
Output: 5
Explanation: If you choose startValue = 4, in the third iteration your step by step sum is less than 1.
                step by step sum
                startValue = 4 | startValue = 5 | nums
                  (4 -3 ) = 1  | (5 -3 ) = 2    |  -3
                  (1 +2 ) = 3  | (2 +2 ) = 4    |   2
                  (3 -3 ) = 0  | (4 -3 ) = 1    |  -3
                  (0 +4 ) = 4  | (1 +4 ) = 5    |   4
                  (4 +2 ) = 6  | (5 +2 ) = 7    |   2
```
**Example 2:**
```
Input: nums = [1,2]
Output: 1
Explanation: Minimum start value should be positive.
```
**Example 3:**
```
Input: nums = [1,-2,-3]
Output: 5
```

**Constraints:**
- 1 <= nums.length <= 100
- -100 <= nums[i] <= 100

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minStartValue(self, nums: List[int]) -> int:
        min_sum = current = 0
        for n in nums:
            current += n
            min_sum = min(min_sum, current)
        return -min_sum + 1
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func minStartValue(nums []int) int {
    min := 0
    sum := 0
    for _, v := range nums {
        sum += v
        if sum < min {
            min = sum
        }
    }
    return -min + 1
}
{{< / highlight >}}
</div>
</div>
