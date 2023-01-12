---
weight: 818
title: "818 Race Car"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp"]
---

Your car starts at position `0` and speed `+1` on an infinite number line. Your car can go into negative positions. Your car drives automatically according to a sequence of instructions `'A'` (accelerate) and `'R'` (reverse):
- When you get an instruction `'A'`, your car does the following:
  - `position += speed`
  - `speed *= 2`
- When you get an instruction `'R'`, your car does the following:
  - If your speed is positive then `speed = -1`
  - otherwise `speed = 1`
  - Your position stays the same.

For example, after commands `"AAR"`, your car goes to positions `0 --> 1 --> 3 --> 3`, and your speed goes to `1 --> 2 --> 4 --> -1`.

Given a target position `target`, return _the length of the shortest sequence of instructions to get there_.


**Example 1:**
```
Input: target = 3
Output: 2
Explanation: 
The shortest instruction sequence is "AA".
Your position goes from 0 --> 1 --> 3.
```
**Example 2:**
```
Input: target = 6
Output: 5
Explanation: 
The shortest instruction sequence is "AAARA".
Your position goes from 0 --> 1 --> 3 --> 7 --> 7 --> 6.
```

**Constraints:**
- <code>1 <= target <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:

    def __init__(self) -> None:
        self.dp = {0: 0}

    def racecar(self, target: int) -> int:
        if target in self.dp:
            return self.dp[target]

        n = target.bit_length()
        if 2**n - 1 == target:
            self.dp[target] = n
        else:
            # 2^(n-1)-1 < i < 2^n-1
            # Strategy 1: go pass target (n)
            #             reverse (1)
            #             continue with the distance (2^n - 1 - target)
            self.dp[target] = n + 1 + self.racecar(2**n - 1 - target)
            # Strategy 2: go as far as possible before pass target (n-1)
            #             reverse (1)
            #             continue m 'A' (m)
            #             reverse again (1)
            #             continue with the distance (target - 2^(n-1) + 2^m)
            for m in range(n - 1):
                self.dp[target] = min(
                    self.dp[target],
                    (n-1) + 1 + m + 1 + self.racecar(target - 2**(n-1) + 2**m)
                )
        
        return self.dp[target]
{{< / highlight >}}
</div>
</div>
