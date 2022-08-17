---
weight: 2104
title: "2104 Sum of Subarray Ranges"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium"]
---

You are given an integer array `nums`. The **range** of a subarray of `nums` is the difference between the largest and smallest element in the subarray.

Return _the **sum of all** subarray ranges of `nums`_.

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**
```
Input: nums = [1,2,3]
Output: 4
Explanation: The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0 
[2], range = 2 - 2 = 0
[3], range = 3 - 3 = 0
[1,2], range = 2 - 1 = 1
[2,3], range = 3 - 2 = 1
[1,2,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 1 + 1 + 2 = 4.
```
**Example 2:**
```
Input: nums = [1,3,3]
Output: 4
Explanation: The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0
[3], range = 3 - 3 = 0
[3], range = 3 - 3 = 0
[1,3], range = 3 - 1 = 2
[3,3], range = 3 - 3 = 0
[1,3,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 2 + 0 + 2 = 4.
```
**Example 3:**
```
Input: nums = [4,-2,-3,4,1]
Output: 59
Explanation: The sum of all subarray ranges of nums is 59.
```

**Constraints:**
- `1 <= nums.length <= 1000`
- <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
 

**Follow-up:** Could you find a solution with O(n) time complexity?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
'''
O(n^2)
'''

class Solution:
    def subArrayRanges(self, nums: List[int]) -> int:
        res = 0
        for i in range(len(nums)):
            min_val = max_val = nums[i]
            for j in range(i, len(nums)):
                min_val = min(min_val, nums[j])
                max_val = max(max_val, nums[j])
                res += (max_val - min_val)
        return res


'''
O(n)
'''
class Solution:
    def subArrayRanges(self, nums: List[int]) -> int:
        def get_sum(op):
            total = 0
            stack = []
            for i in range(len(nums) + 1):
                # Between left boundary and right boundary
                # nums[x] is the largest/smallest element
                while stack and (i == len(nums) or op(nums[i], nums[stack[-1]])):
                    mid = stack.pop()
                    right_boundary = i
                    left_boundary = stack[-1] if stack else -1
                    total += nums[mid] * (right_boundary - mid) * (mid - left_boundary)
                stack.append(i)
            return total
        max_sum = get_sum(lambda x, y: x > y)
        min_sum = get_sum(lambda x, y: x < y)
        return max_sum - min_sum
{{< / highlight >}}
</div>
</div>
