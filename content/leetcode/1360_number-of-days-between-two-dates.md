---
weight: 1360
title: "1360 Number of Days Between Two Dates"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy"]
---

Write a program to count the number of days between two dates.

The two dates are given as strings, their format is `YYYY-MM-DD` as shown in the examples.

**Example 1:**
```
Input: date1 = "2019-06-29", date2 = "2019-06-30"
Output: 1
```
**Example 2:**
```
Input: date1 = "2020-01-15", date2 = "2019-12-31"
Output: 15
```

**Constraints:**
- The given dates are valid dates between the years `1971` and `2100`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def daysBetweenDates(self, date1: str, date2: str) -> int:
        leap = lambda y: bool(y % 400 == 0 or (y % 4 == 0 and y % 100))
        days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
        
        def days_till(date):
            y, m, d = map(int, date.split('-'))
            full_year_days = 365 * (y - 1971) + sum(map(leap, range(1971, y)))
            return full_year_days + d + sum(days[:m-1]) + (m > 2 and leap(y))
        
        return abs(days_till(date1) - days_till(date2))
{{< / highlight >}}
</div>
</div>
