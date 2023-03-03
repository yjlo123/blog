---
weight: 179
title: "179 Largest Number"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_sorting", "lc_greedy"]
---

Given a list of non-negative integers `nums`, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.


**Example 1:**
```
Input: nums = [10,2]
Output: "210"
```
**Example 2:**
```
Input: nums = [3,30,34,5,9]
Output: "9534330"
```

**Constraints:**
- `1 <= nums.length <= 100`
- <code>0 <= nums[i] <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class LargeNumKey(str):
    def __lt__(x, y):
        return x+y > y+x

class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        num = ''.join(sorted(
                        map(str, nums),
                        key=LargeNumKey))
        return '0' if num[0] == '0' else num


'''
Using `cmp_to_key`
'''
from functools import cmp_to_key

class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        def cmp(x, y):
            return -1 if x+y > y+x else 1

        num = ''.join(sorted(
                        map(str, nums),
                        key=cmp_to_key(cmp)))

        return '0' if num[0] == '0' else num
{{< / highlight >}}
</div>
</div>
