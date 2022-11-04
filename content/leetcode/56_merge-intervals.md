---
weight: 56
title: "56 Merge Intervals"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array"]
---

Given an array of `intervals` where<code> intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**
```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```
**Example 2:**
```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**Constraints:**
- <code>1 <= intervals.length <= 10<sup>4</sup></code>
- `intervals[i].length == 2`
- <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        sorted_intervals = sorted(intervals, key=lambda x: x[0])
        res = []
        start, end = sorted_intervals[0]
        for i_start, i_end in sorted_intervals:
            if i_start <= end:
                end = max(end, i_end)
            else:
                res.append([start, end])
                start, end = i_start, i_end
        res.append([start, end])
        return res
{{< / highlight >}}
</div>
</div>
