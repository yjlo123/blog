---
weight: 370
title: "370 Range Addition"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_prefix_sum"]
---

You are given an integer `length` and an array `updates` where <code>updates[i] = [startIdx<sub>i</sub>, endIdx<sub>i</sub>, inc<sub>i</sub>]</code>.

You have an array `arr` of length `length` with all zeros, and you have some operation to apply on `arr`. In the <code>i<sup>th</sup></code> operation, you should increment all the elements <code>arr[startIdx<sub>i</sub>], arr[startIdx<sub>i</sub> + 1], ..., arr[endIdx<sub>i</sub>]</code> by <code>inc<sub>i</sub></code>.

Return _`arr` after applying all the `update`_.

**Example 1:**
```
 0 0 0 0 0
 0 2 2 2 0
 0 2 5 5 3
-2 0 3 5 3
Input: length = 5, updates = [[1,3,2],[2,4,3],[0,2,-2]]
Output: [-2,0,3,5,3]
```
Example 2:
```
Input: length = 10, updates = [[2,4,6],[5,6,8],[1,9,-4]]
Output: [0,-4,2,2,2,4,4,-4,-4,-4]
```

**Constraints:**
- <code>1 <= length <= 10<sup>5</sup></code>
- <code>0 <= updates.length <= 10<sup>4</sup></code>
- <code>0 <= startIdx<sub>i</sub> <= endIdx<sub>i</sub> < length</code>
- <code>-1000 <= inc<sub>i</sub> <= 1000</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def getModifiedArray(
        self,
        length: int,
        updates: List[List[int]]
    ) -> List[int]:
        res = [0] * length
        for u in updates:
            res[u[0]] += u[2]
            if u[1] < length - 1:
                res[u[1] + 1] -= u[2]

        for i in range(1, length):
            res[i] += res[i - 1]
        return res
{{< / highlight >}}
</div>
</div>
