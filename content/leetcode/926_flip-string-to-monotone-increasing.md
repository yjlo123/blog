---
weight: 926
title: "926 Flip String to Monotone Increasing"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

A binary string is monotone increasing if it consists of some number of `0`'s (possibly none), followed by some number of `1`'s (also possibly none).

You are given a binary string `s`. You can flip `s[i]` changing it from `0` to `1` or from `1` to `0`.

Return _the minimum number of flips to make `s` monotone increasing._

**Example 1:**
```
Input: s = "00110"
Output: 1
Explanation: We flip the last digit to get 00111.
```
**Example 2:**
```
Input: s = "010110"
Output: 2
Explanation: We flip to get 011111, or alternatively 000111.
```
**Example 3:**
```
Input: s = "00011000"
Output: 2
Explanation: We flip to get 00000000.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s[i]` is either `'0'` or `'1'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minFlipsMonoIncr(self, s: str) -> int:
        min_flips = flips = s.count('0')
        for c in s:
            if c == '1':
                flips += 1
            else:
                flips -= 1
                min_flips = min(min_flips, flips)
        return min_flips
{{< / highlight >}}
</div>
</div>
