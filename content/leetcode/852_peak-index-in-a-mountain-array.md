---
weight: 852
title: "852 Peak Index in a Mountain Array"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_binary_search"]
---

An array `arr` **a mountain** if the following properties hold:
- `arr.length >= 3`
- There exists some `i` with `0 < i < arr.length - 1` such that:
  - `arr[0] < arr[1] < ... < arr[i - 1] < arr[i]`
  - `arr[i] > arr[i + 1] > ... > arr[arr.length - 1]`

Given a mountain array `arr`, return the index `i` such that `arr[0] < arr[1] < ... < arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1]`.

You must solve it in `O(log(arr.length))` time complexity.

**Example 1:**
```
Input: arr = [0,1,0]
Output: 1
```
**Example 2:**
```
Input: arr = [0,2,1,0]
Output: 1
```
**Example 3:**
```
Input: arr = [0,10,5,2]
Output: 1
```

**Constraints:**
- <code>3 <= arr.length <= 10<sup>5</sup></code>
- <code>0 <= arr[i] <= 10<sup>6</sup></code>
- `arr` is **guaranteed** to be a mountain array.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def peakIndexInMountainArray(self, arr: List[int]) -> int:
        l, r = 0, len(arr) - 1
        while l < r:
            mid = l + (r - l) // 2
            if arr[mid] < arr[mid+1]:
                l = mid + 1
            else:
                r = mid
        return l
{{< / highlight >}}
</div>
</div>
