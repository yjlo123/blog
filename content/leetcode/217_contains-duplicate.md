---
weight: 217
title: "217 Contains Duplicate"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

**Example 1:**
```
Input: nums = [1,2,3,1]
Output: true
```
**Example 2:**
```
Input: nums = [1,2,3,4]
Output: false
```
**Example 3:**
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

**Constraints:**
- 1 <= nums.length <= 10<sup>5</sup>
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(set(nums)) != len(nums)
{{< / highlight >}}
</div>
</div>
