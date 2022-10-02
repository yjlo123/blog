---
weight: 410
title: "410 Split Array Largest Sum"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_binary_search"]
---

Given an array `nums` which consists of non-negative integers and an integer `m`, you can split the array into `m` non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these `m` subarrays.

**Example 1:**
```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```
**Example 2:**
```
Input: nums = [1,2,3,4,5], m = 2
Output: 9
```
**Example 3:**
```
Input: nums = [1,4,4], m = 3
Output: 4
```

**Constraints:**
- `1 <= nums.length <= 1000`
- <code>0 <= nums[i] <= 10<sup>6</sup></code>
- `1 <= m <= min(50, nums.length)`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def splitArray(self, nums: List[int], m: int) -> int:
        def min_subarrays_required(max_sum_allowed: int) -> int:
            current_sum = 0
            splits_required = 0
            
            for element in nums:
                # Add element only if the sum doesn't exceed max_sum_allowed
                if current_sum + element <= max_sum_allowed:
                    current_sum += element
                else:
                    # If the element addition makes sum more than max_sum_allowed
                    # Increment the splits required and reset sum
                    current_sum = element
                    splits_required += 1

            # Return the number of subarrays, which is the number of splits + 1
            return splits_required + 1
        
        # Define the left and right boundary of binary search
        left = max(nums)
        right = sum(nums)
        while left <= right:
            # Find the mid value
            max_sum_allowed = (left + right) // 2
            
            # Find the minimum splits. If splits_required is less than
            # or equal to m move towards left i.e., smaller values
            if min_subarrays_required(max_sum_allowed) <= m:
                right = max_sum_allowed - 1
                minimum_largest_split_sum = max_sum_allowed
            else:
                # Move towards right if splits_required is more than m
                left = max_sum_allowed + 1
        
        return minimum_largest_split_sum
{{< / highlight >}}
</div>
</div>
