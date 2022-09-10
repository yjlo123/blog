---
weight: 35
title: "35 Search Insert Position"
date: 2021-09-18T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_binary_search"]
---

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**
```
Input: nums = [1,3,5,6], target = 5
Output: 2
```
**Example 2:**
```
Input: nums = [1,3,5,6], target = 2
Output: 1
```
**Example 3:**
```
Input: nums = [1,3,5,6], target = 7
Output: 4
```
**Example 4:**
```
Input: nums = [1,3,5,6], target = 0
Output: 0
```
**Example 5:**
```
Input: nums = [1], target = 0
Output: 0
```

**Constraints:**
- <code>1 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `nums` contains **distinct** values sorted in **ascending** order.
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low = 0
        high = len(nums) - 1
        while low <= high:
            mid = low + (high - low) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                low = mid + 1
            else:
                high = mid - 1
        return -1
{{< / highlight >}}
</div>
</div>
