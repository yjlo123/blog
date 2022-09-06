---
weight: 1492
title: "1492 The kth Factor of n"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_math"]
---

You are given two positive integers `n` and `k`. A factor of an integer `n` is defined as an integer `i` where `n % i == 0`.

Consider a list of all factors of `n` sorted in **ascending order**, return the <code>k<sup>th</sup></code> factor in this list or return `-1` if n has less than `k` factors.

**Example 1:**
```
Input: n = 12, k = 3
Output: 3
Explanation: Factors list is [1, 2, 3, 4, 6, 12], the 3rd factor is 3.
```
**Example 2:**
```
Input: n = 7, k = 2
Output: 7
Explanation: Factors list is [1, 7], the 2nd factor is 7.
```
**Example 3:**
```
Input: n = 4, k = 4
Output: -1
Explanation: Factors list is [1, 2, 4], there is only 3 factors. We should return -1.
```

**Constraints:**
- `1 <= k <= n <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def kthFactor(self, n: int, k: int) -> int:
        divisors, sqrt_n = [], int(n**0.5)
        for x in range(1, sqrt_n+1):
            if n % x == 0:
                k -= 1
                if k == 0:
                    return x
                divisors.append(x)
        if sqrt_n * sqrt_n == n:
            k += 1
        if k <= len(divisors):
            return n // divisors[-k]
        else:
            return -1
{{< / highlight >}}
</div>
</div>
