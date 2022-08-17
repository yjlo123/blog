---
weight: 1710
title: "1710 Maximum Units on a Truck"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_greedy", "lc_heap"]
---

You are assigned to put some amount of boxes onto **one truck**. You are given a 2D array `boxTypes`, where boxTypes[i] = [numberOfBoxes<sub>i</sub>, numberOfUnitsPerBox<sub>i</sub>]:

- numberOfBoxes<sub>i</sub> is the number of boxes of type `i`.
- numberOfUnitsPerBox<sub>i</sub> is the number of units in each box of the type `i`.
You are also given an integer `truckSize`, which is the **maximum** number of **boxes** that can be put on the truck. You can choose any boxes to put on the truck as long as the number of boxes does not exceed `truckSize`.

Return the **maximum** total number of **units** that can be put on the truck.

**Example 1:**
```
Input: boxTypes = [[1,3],[2,2],[3,1]], truckSize = 4
Output: 8
Explanation: There are:
- 1 box of the first type that contains 3 units.
- 2 boxes of the second type that contain 2 units each.
- 3 boxes of the third type that contain 1 unit each.
You can take all the boxes of the first and second types,
and one box of the third type.
The total number of units will be = (1 * 3) + (2 * 2) + (1 * 1) = 8.
```

**Example 2:**
```
Input: boxTypes = [[5,10],[2,5],[4,7],[3,9]], truckSize = 10
Output: 91
```

**Constraints:**
- `1 <= boxTypes.length <= 1000`
- <code>1 <= numberOfBoxes<sub>i</sub>, numberOfUnitsPerBox<sub>i</sub> <= 1000</code>
- <code>1 <= truckSize <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from heapq import heappush, heappop

class Solution:
    def maximumUnits(self, boxTypes: List[List[int]], truckSize: int) -> int:
        h = []
        for bt in boxTypes:
            heappush(h, (-bt[1], bt[0]))
        unit_count = 0
        while h and truckSize > 0:
            top = heappop(h)
            box_count = min(truckSize, top[1])
            unit_count += (-top[0]) * box_count
            truckSize -= box_count
        return unit_count
{{< / highlight >}}
</div>
</div>
