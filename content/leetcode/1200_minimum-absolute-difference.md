---
weight: 1200
title: "1200 Minimum Absolute Difference"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array", "lc_sorting"]
---

Given an array of **distinct** integers `arr`, find all pairs of elements with the minimum absolute difference of any two elements.

Return a list of pairs in ascending order(with respect to pairs), each pair `[a, b]` follows

- `a, b` are from `arr`
- `a < b`
- `b - a` equals to the minimum absolute difference of any two elements in `arr`
 

**Example 1:**
```
Input: arr = [4,2,1,3]
Output: [[1,2],[2,3],[3,4]]
Explanation: The minimum absolute difference is 1.
List all pairs with difference equal to 1 in ascending order.
```
**Example 2:**
```
Input: arr = [1,3,6,10,15]
Output: [[1,3]]
```
**Example 3:**
```
Input: arr = [3,8,-10,23,19,-4,-14,27]
Output: [[-14,-10],[19,23],[23,27]]
```

**Constraints:**
- <code>2 <= arr.length <= 10<sup>5</sup></code>
- <code>-10<sup>5</sup> <= arr[i] <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
import math

class Solution:
    def minimumAbsDifference(self, arr: List[int]) -> List[List[int]]:
        res = []
        min_diff = math.inf
        arr.sort()
        for i in range(1, len(arr)):
            diff = arr[i] - arr[i-1]
            if diff < min_diff:
                res = [[arr[i-1], arr[i]]]
                min_diff = diff
            elif diff == min_diff:
                res.append([arr[i-1], arr[i]])
        return res
{{< / highlight >}}
</div>
</div>
