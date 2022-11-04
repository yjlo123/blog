---
weight: 2276
title: "2276 Count Integers in Intervals"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_binary_search"]
---

Given an **empty** set of intervals, implement a data structure that can:
- **Add** an interval to the set of intervals.
- **Count** the number of integers that are present in **at least one** interval.

Implement the `CountIntervals` class:
- `CountIntervals()` Initializes the object with an empty set of intervals.
- `void add(int left, int right)` Adds the interval `[left, right]` to the set of intervals.
- `int count()` Returns the number of integers that are present in **at least one** interval.

**Note** that an interval `[left, right]` denotes all the integers `x` where `left <= x <= right`.

**Example 1:**
```
Input
["CountIntervals", "add", "add", "count", "add", "count"]
[[], [2, 3], [7, 10], [], [5, 8], []]
Output
[null, null, null, 6, null, 8]

Explanation
CountIntervals countIntervals = new CountIntervals(); // initialize the object with an empty set of intervals. 
countIntervals.add(2, 3);  // add [2, 3] to the set of intervals.
countIntervals.add(7, 10); // add [7, 10] to the set of intervals.
countIntervals.count();    // return 6
                           // the integers 2 and 3 are present in the interval [2, 3].
                           // the integers 7, 8, 9, and 10 are present in the interval [7, 10].
countIntervals.add(5, 8);  // add [5, 8] to the set of intervals.
countIntervals.count();    // return 8
                           // the integers 2 and 3 are present in the interval [2, 3].
                           // the integers 5 and 6 are present in the interval [5, 8].
                           // the integers 7 and 8 are present in the intervals [5, 8] and [7, 10].
                           // the integers 9 and 10 are present in the interval [7, 10].
```

**Constraints:**
- <code>1 <= left <= right <= 10<sup>9</sup></code>
- At most <code>10<sup>5</sup></code> calls **in total** will be made to `add` and `count`.
- At least **one** call will be made to `count`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from math import inf
import bisect

class CountIntervals:

    def __init__(self):
        self.intervals = [(-inf, -inf), (inf, inf)]
        self.cnt = 0

    def add(self, left: int, right: int) -> None:
        li  = bisect.bisect_left(self.intervals, left-1, key=lambda x: x[1])
        lv = min(self.intervals[li][0], left)
        
        ri = bisect.bisect_right(self.intervals, right+1, key=lambda x: x[0])
        rv = max(self.intervals[ri-1][1], right)

        to_del = 0
        for i in range(li, ri):
            to_del += (self.intervals[i][1] - self.intervals[i][0] + 1)
        
        self.cnt += (rv - lv + 1 - to_del)
        self.intervals[li:ri] = [(lv, rv)]

    def count(self) -> int:
        return self.cnt


# Your CountIntervals object will be instantiated and called as such:
# obj = CountIntervals()
# obj.add(left,right)
# param_2 = obj.count()
{{< / highlight >}}
</div>
</div>
