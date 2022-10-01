---
weight: 461
title: "461 Hamming Distance"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy"]
---

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x` and `y`, return the Hamming distance between them.

**Example 1:**
```
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
The above arrows point to positions where the corresponding bits are different.
```
**Example 2:**
```
Input: x = 3, y = 1
Output: 1
```

**Constraints:**

- <code>0 <= x, y <= 2<sup>31</sup> - 1</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        count = 0
        while x > 0 or y > 0:
            count += (x & 1) ^ (y & 1)
            x >>= 1
            y >>= 1
        return count


'''
One line
'''
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        return bin(x ^ y).count('1')
{{< / highlight >}}
</div>
</div>
