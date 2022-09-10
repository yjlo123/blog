---
weight: 253
title: "253 Meeting Rooms II"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_greedy"]
---

Given an array of meeting time `intervals` intervals where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, return _the minimum number of conference rooms required_.

**Example 1:**
```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: 2
```

**Example 2:**
```
Input: intervals = [[7,10],[2,4]]
Output: 1
```

**Constraints:**
- <code>1 <= intervals.length <= 10<sup>4</sup></code>
- <code>0 <= start<sub>i</sub> < end<sub>i</sub> <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        free_rooms = []
        intervals.sort(key=lambda t: t[0])
        
        heapq.heappush(free_rooms, intervals[0][1])
        
        for i in intervals[1:]:
            if free_rooms[0] <= i[0]:
                heapq.heappop(free_rooms)
            heapq.heappush(free_rooms, i[1])

        return len(free_rooms)
{{< / highlight >}}
</div>
</div>
