---
weight: 1229
title: "1229 Meeting Scheduler"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_two_pointers"]
---

Given the availability time slots arrays `slots1` and `slots2` of two people and a meeting duration `duration`, return the **earliest time slot** that works for both of them and is of duration `duration`.

If there is no common time slot that satisfies the requirements, return an **empty array**.

The format of a time slot is an array of two elements `[start, end]` representing an inclusive time range from `start` to `end`.

It is guaranteed that no two availability slots of the same person intersect with each other. That is, for any two time slots `[start1, end1]` and `[start2, end2]` of the same person, either `start1 > end2` or `start2 > end1`.

**Example 1:**
```
Input: slots1 = [[10,50],[60,120],[140,210]], slots2 = [[0,15],[60,70]], duration = 8
Output: [60,68]
```
**Example 2:**
```
Input: slots1 = [[10,50],[60,120],[140,210]], slots2 = [[0,15],[60,70]], duration = 12
Output: []
```

**Constraints:**
- <code>1 <= slots1.length, slots2.length <= 10<sup>4</sup></code>
- `slots1[i].length, slots2[i].length == 2`
- `slots1[i][0] < slots1[i][1]`
- `slots2[i][0] < slots2[i][1]`
- <code>0 <= slots1[i][j], slots2[i][j] <= 10<sup>9</sup></code>
- <code>1 <= duration <= 10<sup>6</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minAvailableDuration(
        self,
        slots1: List[List[int]],
        slots2: List[List[int]],
        duration: int
    ) -> List[int]:
        slots1.sort()
        slots2.sort()
        m, n = len(slots1), len(slots2)
        i, j = 0, 0
        while i < m and j < n:
            start = max(slots1[i][0], slots2[j][0])
            end = min(slots1[i][1], slots2[j][1])
            if end - start >= duration:
                return [start, start + duration]
            if slots1[i][1] < slots2[j][1]:
                i += 1
            else:
                j += 1
        return []
{{< / highlight >}}
</div>
</div>
