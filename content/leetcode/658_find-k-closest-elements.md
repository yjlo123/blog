---
weight: 658
title: "658 Find K Closest Elements"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_binary_search", "lc_two_pointers"]
---

Given a sorted integer array `arr`, two integers `k` and `x`, return the `k` closest integers to `x` in the array. The result should also be sorted in ascending order.

An integer `a` is closer to `x` than an integer `b` if:

- `|a - x| < |b - x|`, or
- `|a - x| == |b - x|` and `a < b`

**Example 1:**
```
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```
**Example 2:**
```
Input: arr = [1,2,3,4,5], k = 4, x = -1
Output: [1,2,3,4]
```

**Constraints:**
- `1 <= k <= arr.length`
- <code>1 <= arr.length <= 10<sup>4</sup></code>
- `arr` is sorted in **ascending** order.
- <code>-10<sup>4</sup> <= arr[i], x <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
import bisect

class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        i = bisect.bisect_left(arr, x)
        l, r = i - 1, i
        while r - l <= k:
            if l == -1:
                r += 1
            elif r == len(arr) or abs(arr[l] - x) <= abs(arr[r] - x):
                l -= 1
            else:
                r += 1
        return arr[l+1:r]


'''
Binary search for the left boundary
'''
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        '''
        If the element at arr[mid] is closer to x than arr[mid + k],
        then that means arr[mid + k], as well as every element to
        the right of it can never be in the answer. This means we
        should move our right pointer to avoid considering them.
        The logic is the same vice-versa - if arr[mid + k] is
        closer to x, then move the left pointer.
        '''
        # Initialize binary search bounds
        left = 0
        right = len(arr) - k
        
        # Binary search against the criteria described
        while left < right:
            mid = (left + right) // 2
            if x - arr[mid] > arr[mid + k] - x:
                left = mid + 1
            else:
                right = mid

        return arr[left:left + k]
{{< / highlight >}}
</div>
</div>
