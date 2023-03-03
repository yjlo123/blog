---
weight: 907
title: "907 Sum of Subarray Minimums"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack", "lc_array"]
---

Given an array of integers `arr`, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer modulo <code>10<sup>9</sup> + 7</code>.

**Example 1:**
```
Input: arr = [3,1,2,4]
Output: 17
Explanation: 
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4]. 
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.
```
**Example 2:**
```
Input: arr = [11,81,94,43,3]
Output: 444
```

**Constraints:**
- <code>1 <= arr.length <= 3 * 10<sup>4</sup></code>
- <code>1 <= arr[i] <= 3 * 10<sup>4</sup></code>

> For each element, find how many subarrays containing this element with this element as the minimum.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def sumSubarrayMins(self, arr: List[int]) -> int:
        MIN_VAL = float('-inf')
        MOD = 10**9 + 7
        res = 0
        stack = []  #  non-decreasing 
        arr = [MIN_VAL] + arr + [MIN_VAL]
        for i, n in enumerate(arr):
            while stack and arr[stack[-1]] > n:
                cur = stack.pop()
                # arr[cur] is the min between arr[stack[-1]] and arr[i] (exclusive)
                res += arr[cur] * (cur - stack[-1]) * (i - cur) 
            stack.append(i)
        return res % MOD
{{< / highlight >}}
</div>
</div>
