---
weight: 136
title: "136 Single Number"
date: 2020-09-26T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_hash_table"]
---

Given a **non-empty** array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

**Example 1:**
```
Input: [2,2,1]
Output: 1
```
**Example 2:**
```
Input: [4,1,2,1,2]
Output: 4
```
**Example 3:**
```
Input: nums = [1]
Output: 1
```

**Constraints:**
- <code>1 <= nums.length <= 3 * 10<sup>4</sup></code>
- <code>-3 * 10<sup>4</sup> <= nums[i] <= 3 * 10<sup>4</sup></code>
- Each element in the array appears twice except for one element which appears only once.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        s = set()
        for num in nums:
            if num in s:
                s.remove(num)
            else:
                s.add(num)
        return list(s)[0]

"""
Math
"""
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return 2 * sum(set(nums)) - sum(nums)

{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func singleNumber(nums []int) int {
    set := make(map[int]bool)
    for _, num := range nums {
        if _, ok := set[num]; ok {
            delete(set, num)
        } else {
            set[num] = true
        }
    }
    for num, _ := range set {
        return num
    }
    return -1
}
{{< / highlight >}}
</div>

<div id="runtime" class="lang">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode136" target="_blank">https://runtime.siwei.dev/?src=leetcode136</a>
    </div>
</div>
</div>
