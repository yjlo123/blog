---
weight: 1480
title: "1480 Running Sum of 1d Array"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

Given an array `nums`. We define a running sum of an array as `runningSum[i] = sum(nums[0]…nums[i])`.

Return _the running sum of `nums`_.

**Example 1:**
```
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
Explanation: Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].
```
**Example 2:**
```
Input: nums = [1,1,1,1,1]
Output: [1,2,3,4,5]
Explanation: Running sum is obtained as follows:
[1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1].
```
**Example 3:**
```
Input: nums = [3,1,2,10,1]
Output: [3,4,6,16,17]
```

**Constraints:**
- `1 <= nums.length <= 1000`
- <code>-10<sup>6</sup> <= nums[i] <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        for i in range(1, len(nums)):
            nums[i] += nums[i-1]
        return nums
{{< / highlight >}}
</div>
</div>
