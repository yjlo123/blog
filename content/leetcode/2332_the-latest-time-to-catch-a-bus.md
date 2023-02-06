---
weight: 2332
title: "2332 The Latest Time to Catch a Bus"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium"]
---

You are given a **0-indexed** integer array `buses` of length `n`, where `buses[i]` represents the departure time of the <code>i<sup>th</sup></code> bus. You are also given a **0-indexed** integer array `passengers` of length `m`, where `passengers[j]` represents the arrival time of the <code>j<sup>th</sup></code> passenger. All bus departure times are unique. All passenger arrival times are unique.

You are given an integer `capacity`, which represents the **maximum** number of passengers that can get on each bus.

When a passenger arrives, they will wait in line for the next available bus. You can get on a bus that departs at `x` minutes if you arrive at `y` minutes where `y <= x`, and the bus is not full. Passengers with the **earliest** arrival times get on the bus first.

More formally when a bus arrives, either:
- If `capacity` or fewer passengers are waiting for a bus, they will all get on the bus, or
- The `capacity` passengers with the earliest arrival times will get on the bus.

Return *the latest time you may arrive at the bus station to catch a bus*. You **cannot** arrive at the same time as another passenger.

**Note**: The arrays `buses` and `passengers` are not necessarily sorted.

**Example 1:**
```
Input: buses = [10,20], passengers = [2,17,18,19], capacity = 2
Output: 16
Explanation: Suppose you arrive at time 16.
At time 10, the first bus departs with the 0th passenger. 
At time 20, the second bus departs with you and the 1st passenger.
Note that you may not arrive at the same time as another passenger,
which is why you must arrive before the 1st passenger to catch the bus.
```
**Example 2:**
```
Input: buses = [20,30,10], passengers = [19,13,26,4,25,11,21], capacity = 2
Output: 20
Explanation: Suppose you arrive at time 20.
At time 10, the first bus departs with the 3rd passenger. 
At time 20, the second bus departs with the 5th and 1st passengers.
At time 30, the third bus departs with the 0th passenger and you.
Notice if you had arrived any later, then the 6th passenger would have taken
your seat on the third bus.
```

**Constraints:**
- `n == buses.length`
- `m == passengers.length`
- <code>1 <= n, m, capacity <= 10<sup>5</sup></code>
- <code>2 <= buses[i], passengers[i] <= 10<sup>9</sup></code>
- Each element in `buses` is **unique**.
- Each element in `passengers` is **unique**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def latestTimeCatchTheBus(
        self,
        buses: List[int],
        passengers: List[int],
        capacity: int
    ) -> int:
        i = 0
        passengers.sort()
        curr_bus = 0
        for bus in sorted(buses):
            curr_bus = 0
            while (
                i < len(passengers) and
                passengers[i] <= bus and
                curr_bus < capacity
            ):
                curr_bus += 1
                i += 1

        # check last bus
        last = bus if curr_bus < capacity else passengers[i-1]
        while passengers[i-1] == last:
            last -= 1
            i -= 1
        return last
{{< / highlight >}}
</div>
</div>
