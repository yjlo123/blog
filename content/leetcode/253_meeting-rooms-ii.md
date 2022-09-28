---
weight: 253
title: "253 Meeting Rooms II"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_greedy", "lc_heap", "lc_sorting"]
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
'''
Priority Queues
'''
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        used_rooms = []
        intervals.sort(key=lambda t: t[0])
        
        heapq.heappush(used_rooms, intervals[0][1])
        
        for i in intervals[1:]:
            if used_rooms[0] <= i[0]:
                heapq.heappop(used_rooms)
            heapq.heappush(used_rooms, i[1])

        return len(used_rooms)

'''
Chronological Ordering
'''
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        if not intervals:
            return 0

        used_rooms = 0
        start_timings = sorted([i[0] for i in intervals])
        end_timings = sorted(i[1] for i in intervals)

        L = len(intervals)
        end_pointer = 0
        start_pointer = 0
        while start_pointer < L:
            if start_timings[start_pointer] >= end_timings[end_pointer]:
                used_rooms -= 1
                end_pointer += 1
            used_rooms += 1    
            start_pointer += 1   

        return used_rooms
{{< / highlight >}}
</div>
</div>
