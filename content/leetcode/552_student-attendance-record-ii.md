---
weight: 552
title: "552 Student Attendance Record II"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp"]
---

An attendance record for a student can be represented as a string where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters:

- `'A'`: Absent.
- `'L'`: Late.
- `'P'`: Present.

Any student is eligible for an attendance award if they meet **both** of the following criteria:

- The student was absent (`'A'`) for **strictly** fewer than 2 days **total**.
- The student was never late (`'L'`) for 3 or more **consecutive** days.

Given an integer `n`, return _the number of possible attendance records of length `n` that make a student eligible for an attendance award. The answer may be very large, so return it modulo_ <code>10<sup>9</sup> + 7</code>.


**Example 1:**
```
Input: n = 2
Output: 8
Explanation: There are 8 records with length 2 that are eligible for an award:
"PP", "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" is not eligible because there are 2 absences (there need to be fewer than 2).
```
**Example 2:**
```
Input: n = 1
Output: 3
```
**Example 3:**
```
Input: n = 10101
Output: 183236316
```

**Constraints:**
- <code>1 <= n <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def checkRecord(self, n: int) -> int:
        MOD = 10 ** 9 + 7

        # dp[n] represents the number of possible
        #       rewardable strings of length n
        #       with L and P as the only characters
        dp = [1,2,4,7] + [0] * (2 if n <= 5 else n-3)
        # dp[i] = 2 * dp[i−1] - dp[i−4]
        #       = (end with P) + (end with L)
        #         - (end with PLLL)

        for i in range(4, n+1):
            dp[i] = (2 * dp[i-1]) % MOD + (MOD-dp[i-4]) % MOD

        # without "A"
        total = dp[n]

        # with  "A"
        for i in range(1, n+1):
            total += (dp[i-1] * dp[n-i]) % MOD

        return total % MOD
{{< / highlight >}}
</div>
</div>
