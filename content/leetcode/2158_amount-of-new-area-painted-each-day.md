---
weight: 2158
title: "2158 Amount of New Area Painted Each Day"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_array", "lc_hash_table"]
---

There is a long and thin painting that can be represented by a number line. You are given a **0-indexed** 2D integer array `paint` of length `n`, where <code>paint[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>. This means that on the <code>i<sup>th</sup></code> day you need to paint the area between <code>start<sub>i</sub></code> and <code>end<sub>i</sub></code>.

Painting the same area multiple times will create an uneven painting so you only want to paint each area of the painting at most **once**.

Return _an integer array `worklog` of length `n`, where `worklog[i]` is the amount of **new** area that you painted on the <code>i<sup>th</sup></code> day_.

**Example 1:**
```
           222   <= x
  00000011111122
0 1 2 3 4 5 6 7 8

Input: paint = [[1,4],[4,7],[5,8]]
Output: [3,3,1]
Explanation:
On day 0, paint everything between 1 and 4.
The amount of new area painted on day 0 is 4 - 1 = 3.
On day 1, paint everything between 4 and 7.
The amount of new area painted on day 1 is 7 - 4 = 3.
On day 2, paint everything between 7 and 8.
Everything between 5 and 7 was already painted on day 1.
The amount of new area painted on day 2 is 8 - 7 = 1. 
```
**Example 2:**
```
          2222   <= x
  00000022111111
0 1 2 3 4 5 6 7 8

Input: paint = [[1,4],[5,8],[4,7]]
Output: [3,3,1]
Explanation:
On day 0, paint everything between 1 and 4.
The amount of new area painted on day 0 is 4 - 1 = 3.
On day 1, paint everything between 5 and 8.
The amount of new area painted on day 1 is 8 - 5 = 3.
On day 2, paint everything between 4 and 5.
Everything between 5 and 7 was already painted on day 1.
The amount of new area painted on day 2 is 5 - 4 = 1. 
```
**Example 3:**
```
    1111   <= x
  00000000
0 1 2 3 4 5

Input: paint = [[1,5],[2,4]]
Output: [4,0]
Explanation:
On day 0, paint everything between 1 and 5.
The amount of new area painted on day 0 is 5 - 1 = 4.
On day 1, paint nothing because everything between 2 and 4 was already painted on day 0.
The amount of new area painted on day 1 is 0.
```

**Constraints:**
- `1 <= paint.length <= 105`
- `paint[i].length == 2`
- <code>0 <= start<sub>i</sub> < end<sub>i</sub> <= 5 * 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def amountPainted(self, paint: List[List[int]]) -> List[int]:
        line = defaultdict(int)
        res = []
        for start, end in paint:
            work = 0
            while start < end:
                jump = max(start + 1, line[start])
                if not line[start]:
                    work += 1
                line[start] = max(line[start], end)
                start = jump
            res.append(work)
        return res
{{< / highlight >}}
</div>
</div>
