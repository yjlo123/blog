---
weight: 390
title: "390 Elimination Game"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array", "lc_math"]
---

You have a list `arr` of all integers in the range `[1, n]` sorted in a strictly increasing order. Apply the following algorithm on `arr`:
- Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.
- Repeat the previous step again, but this time from right to left, remove the rightmost number and every other number from the remaining numbers.
- Keep repeating the steps again, alternating left to right and right to left, until a single number remains.

Given the integer `n`, return _the last number that remains in `arr`_.


**Example 1:**
```
Input: n = 9
Output: 6
Explanation:
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
arr = [2, 4, 6, 8]
arr = [2, 6]
arr = [6]
```
**Example 2:**
```
Input: n = 1
Output: 1
```

**Constraints:**
- <code>1 <= n <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def lastRemaining(self, n: int) -> int:
        def helper(n, from_left):
            if n == 1:
                return 1
            if from_left:
                # remove odd
                return 2 * helper(n // 2, False)
            elif n % 2 == 1:
                # remove odd
                return 2 * helper(n // 2, True)
            else:
                # remove even
                # [1 2 3 4 5 6 ] ==> [1 3 5] == 2 * [1 2 3] - 1
                return 2 * helper(n // 2, True) - 1
        return helper(n, True)
{{< / highlight >}}
</div>
</div>
