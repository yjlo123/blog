---
weight: 935
title: "935 Knight Dialer"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

The chess knight has a **unique movement**, it may move two squares vertically and one square horizontally, or two squares horizontally and one square vertically (with both forming the shape of an **L**). The possible movements of chess knight are shown in this diagaram:

A chess knight can move as indicated in the chess diagram below:

<img src="https://assets.leetcode.com/uploads/2020/08/18/chess.jpg" style="width: 60%;"/>

We have a chess knight and a phone pad as shown below, the knight **can only stand on a numeric cell** (i.e. blue cell).
```
1 2 3
4 5 6
7 8 9
* 0 #
```
Given an integer `n`, return how many distinct phone numbers of length n we can dial.

You are allowed to place the knight **on any numeric cell** initially and then you should perform `n - 1` jumps to dial a number of length `n`. All jumps should be **valid** knight jumps.

As the answer may be very large, **return the answer modulo** <code>10<sup>9</sup> + 7</code>.

**Example 1:**
```
Input: n = 1
Output: 10
Explanation: We need to dial a number of length 1,
so placing the knight over any numeric cell of the 10 cells is sufficient.
```
**Example 2:**
```
Input: n = 2
Output: 20
Explanation: All the valid number we can dial are
[04, 06, 16, 18, 27, 29, 34, 38, 40, 43, 49, 60, 61, 67, 72, 76, 81, 83, 92, 94]
```
**Example 3:**
```
Input: n = 3131
Output: 136006598
Explanation: Please take care of the mod.
```

**Constraints:**
- `1 <= n <= 5000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def knightDialer(self, n: int) -> int:
        MOD = 10**9 + 7
        m = {
            1: [6, 8],
            2: [7, 9],
            3: [4, 8],
            4: [3, 9, 0],
            6: [1, 7, 0],
            5: [],
            7: [2, 6],
            8: [1, 3],
            9: [2, 4],
            0: [4, 6],
        }
        
        current_counts = [1] * 10
        for _ in range(n-1):
            next_counts = [0] * 10
            for src in range(10):
                for dst in m[src]:
                    next_counts[dst] = (next_counts[dst] + current_counts[src]) % MOD
            current_counts = next_counts
        return sum(current_counts) % MOD
{{< / highlight >}}
</div>
</div>
