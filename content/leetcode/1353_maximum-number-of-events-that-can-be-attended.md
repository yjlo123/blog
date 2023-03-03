---
weight: 1353
title: "1353 Maximum Number of Events That Can Be Attended"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_heap", "lc_greedy"]
---

You are given an array of `events` where <code>events[i] = [startDay<sub>i</sub>, endDay<sub>i</sub>]</code>. Every event `i` starts at <code>startDay<sub>i</sub></code> and ends at <code>endDay<sub>i</sub></code>.

You can attend an event `i` at any day `d` where <code>startTime<sub>i</sub> <= d <= endTime<sub>i</sub></code>. You can only attend one event at any time `d`.

Return *the maximum number of events you can attend*.


**Example 1:**
```
 1 [x _]
 2   [x _]
 3     [x _]
Day 1 2 3 4

Input: events = [[1,2],[2,3],[3,4]]
Output: 3
Explanation: You can attend all the three events.
One way to attend them all is as shown.
Attend the first event on day 1.
Attend the second event on day 2.
Attend the third event on day 3.
```
**Example 2:**
```
Input: events= [[1,2],[2,3],[3,4],[1,2]]
Output: 4
```

**Constraints:**
- <code>1 <= events.length <= 10<sup>5</sup></code>
- `events[i].length == 2`
- <code>1 <= startDay<sub>i</sub> <= endDay<sub>i</sub> <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxEvents(self, events: List[List[int]]) -> int:
        n = len(events)
        events.sort()
        heap = []   # heap of on-going events' end time
        res = 0
        d = 0
        i = 0   # index of sorted events

        while i < n or heap:
            # while there are no-yet stated or on-going events

            if not heap:
                # no on-going events, jump to the next event
                d = events[i][0]

            while i < n and events[i][0] <= d:
                # add started events' end time to heap
                heapq.heappush(heap, events[i][1])
                i += 1

            heapq.heappop(heap)
            res += 1
            d += 1
            while heap and heap[0] < d:
                # remove ended events from heap
                heapq.heappop(heap)

        return res
{{< / highlight >}}
</div>
</div>
