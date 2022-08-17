---
weight: 1207
title: "1207 Unique Number of Occurrences"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

Given an array of integers `arr`, return `true` if the number of occurrences of each value in the array is **unique**, or `false` otherwise.

**Example 1:**
```
Input: arr = [1,2,2,1,1,3]
Output: true
Explanation: The value 1 has 3 occurrences, 2 has 2 and 3 has 1.
No two values have the same number of occurrences.
```
**Example 2:**
```
Input: arr = [1,2]
Output: false
```
**Example 3:**
```
Input: arr = [-3,0,1,-3,1,1,1,-3,10,0]
Output: true
```

**Constraints:**
- `1 <= arr.length <= 1000`
- `-1000 <= arr[i] <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def uniqueOccurrences(self, arr: List[int]) -> bool:
        d = {}
        for a in arr:
            d[a] = d.get(a, 0) + 1
        counts = d.values()
        return len(counts) == len(set(counts))
{{< / highlight >}}
</div>
</div>
