---
weight: 977
title: "977 Squares of a Sorted Array"
date: 2021-09-18T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_two_pointers"]
---

Given an integer array `nums` sorted in **non-decreasing** order, return _an array of **the squares of each number** sorted in non-decreasing order_.

 

**Example 1:**
```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```
**Example 2:**
```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

**Constraints:**
- 1 <= nums.length <= 10<sup>4</sup>
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
- `nums` is sorted in non-decreasing order.
 

Follow up: Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [0] * n
        left = 0
        right = n - 1
        
        for i in range(n):
            if abs(nums[left]) < abs(nums[right]):
                num = nums[right]
                right -= 1
            else:
                num = nums[left]
                left += 1
            result[n-i-1] = num * num
        
        return result
{{< / highlight >}}
</div>
</div>
