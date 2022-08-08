---
weight: 357
title: "357 Count Numbers with Unique Digits"
date: 2022-08-07T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium"]
---

Given an integer n, return the count of all numbers with unique digits, x, where 0 <= x < 10n.

**Example 1:**
```
Input: n = 2
Output: 91
Explanation: The answer should be the total numbers in the range of 0 ≤ x < 100,
excluding 11,22,33,44,55,66,77,88,99
```

**Example 2:**
```
Input: n = 0
Output: 1
```

**Constraints:**
- 0 <= n <= 8

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    '''
    <x-digit num: y numbers with unique digits>
    0: 1
    1: 9
    2: 9*9
    3: 9*9*8
    4: 9*9*8*7
    '''
    def countNumbersWithUniqueDigits(self, n: int) -> int:
        res = 1
        acc = 9
        cur = 9
        i = 1
        while i <= n:
            res += acc
            acc *= cur
            cur -= 1
            i += 1
        return res
{{< / highlight >}}
</div>
</div>
