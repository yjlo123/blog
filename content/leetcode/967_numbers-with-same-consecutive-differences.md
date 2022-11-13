---
weight: 967
title: "967 Numbers With Same Consecutive Differences"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bfs"]
---

Given two integers n and k, return _an array of all the integers of length `n` where the difference between every two consecutive digits is `k`_. You may return the answer in **any order**.

Note that the integers should not have leading zeros. Integers as `02` and `043` are not allowed.

**Example 1:**
```
Input: n = 3, k = 7
Output: [181,292,707,818,929]
Explanation: Note that 070 is not a valid number, because it has leading zeroes.
```
**Example 2:**
```
Input: n = 2, k = 1
Output: [10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```

**Constraints:**
- `2 <= n <= 9`
- `0 <= k <= 9`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numsSameConsecDiff(self, n: int, k: int) -> List[int]:
        res = [i for i in range(1, 10)]
        for _ in range(n - 1):
            temp = []
            for num in res:
                last_digit = num % 10
                if last_digit + k < 10:
                    temp.append(num * 10 + last_digit + k)
                if k == 0:
                    continue
                if last_digit - k >= 0:
                    temp.append(num * 10 + last_digit - k)
            res = temp
        return res
{{< / highlight >}}
</div>
</div>
