---
weight: 845
title: "845 Longest Mountain in Array"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array"]
---

You may recall that an array `arr` is **a mountain array** if and only if:

- `arr.length >= 3`
- There exists some index `i` (**0-indexed**) with `0 < i < arr.length - 1` such that:
  - `arr[0] < arr[1] < ... < arr[i - 1] < arr[i]`
  - `arr[i] > arr[i + 1] > ... > arr[arr.length - 1]`

Given an integer array `arr`, return _the length of the longest subarray, which is a mountain_. Return `0` if there is no mountain subarray.

**Example 1:**
```
Input: arr = [2,1,4,7,3,2,5]
Output: 5
Explanation: The largest mountain is [1,4,7,3,2] which has length 5.
```
**Example 2:**
```
Input: arr = [2,2,2]
Output: 0
Explanation: There is no mountain.
```

**Constraints:**
- <code>1 <= arr.length <= 10<sup>4</sup></code>
- <code>0 <= arr[i] <= 10<sup>4</sup></code>

**Follow up:**
- Can you solve it using only one pass?
- Can you solve it in `O(1)` space?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def longestMountain(self, arr: List[int]) -> int:
        n = len(arr)
        up, down = [0] * n, [0] * n

        for i in range(1, n):
            if arr[i] > arr[i - 1]:
                up[i] = up[i - 1] + 1

        for i in range(n-2, -1, -1):
            if arr[i] > arr[i + 1]:
                down[i] = down[i + 1] + 1

        return max(
            [u + d + 1 for u, d in zip(up, down) if u and d]
            or [0]
        )


'''
One pass
'''
class Solution:
    def longestMountain(self, arr: List[int]) -> int:
        n = len(arr)
        res = up = down = 0
        for i in range(1, n):
            if (
                down and arr[i - 1] < arr[i]
                or arr[i - 1] == arr[i]
            ):
                up = down = 0

            up += arr[i - 1] < arr[i]
            down += arr[i - 1] > arr[i]

            if up and down:
                res = max(res, up + down + 1)
        return res
{{< / highlight >}}
</div>
</div>
