---
weight: 1444
title: "1444 Number of Ways of Cutting a Pizza"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp", "lc_prefix_sum"]
---

Given a rectangular pizza represented as a `rows x cols` matrix containing the following characters: `'A'` (an apple) and `'.'` (empty cell) and given the integer `k`. You have to cut the pizza into `k` pieces using `k-1` cuts. 

For each cut you choose the direction: vertical or horizontal, then you choose a cut position at the cell boundary and cut the pizza into two pieces. If you cut the pizza vertically, give the left part of the pizza to a person. If you cut the pizza horizontally, give the upper part of the pizza to a person. Give the last piece of pizza to the last person.

Return _the number of ways of cutting the pizza such that each piece contains **at least** one apple_. Since the answer can be a huge number, return this modulo 10^9 + 7.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/04/23/ways_to_cut_apple_1.png" style="width: 100%;"/>
```
Input: pizza = ["A..","AAA","..."], k = 3
Output: 3 
Explanation: The figure above shows the three ways to cut the pizza.
Note that pieces must contain at least one apple.
```
**Example 2:**
```
Input: pizza = ["A..","AA.","..."], k = 3
Output: 1
```
**Example 3:**
```
Input: pizza = ["A..","A..","..."], k = 1
Output: 1
```

**Constraints:**
- `1 <= rows, cols <= 50`
- `rows == pizza.length`
- `cols == pizza[i].length`
- `1 <= k <= 10`
- `pizza` consists of characters `'A'` and `'.'` only.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def ways(self, pizza: List[str], k: int) -> int:
        m, n = len(pizza), len(pizza[0])
        MOD = 10 ** 9 + 7
        # num of apples in pizza[i:][j:]
        pre_sum = [[0] * (n + 1) for _ in range(m + 1)]
        for i in range(m - 1, -1, -1):
            for j in range(n - 1, -1, -1):
                pre_sum[i][j] = (
                    (1 if pizza[i][j] == 'A' else 0)
                    + pre_sum[i][j+1]
                    + pre_sum[i+1][j]
                    - pre_sum[i+1][j+1]
                )

        memo = {}

        def rec(i, j, cut):
            # rest of pizza: pizza[i:][j:]
            if pre_sum[i][j] == 0:
                # no apple left, 0 way to cut
                return 0
            if cut == 0:
                return 1
            if (i, j, cut) in memo:
                return memo[(i, j, cut)]
            res = 0
            # horizontal, possible to cut at [i+1, m-1]
            for ci in range(i + 1, m):
                # cut at ci
                if pre_sum[i][j] - pre_sum[ci][j] > 0:
                    res += rec(ci, j, cut-1)
                    res %= MOD
            # vertical, possible to cut [j+1, n-1]
            for cj in range(j + 1, n):
                # cut at cj
                if pre_sum[i][j] - pre_sum[i][cj] > 0:
                    res += rec(i, cj, cut-1)
                    res %= MOD
            memo[(i, j, cut)] = res
            return res
        return rec(0, 0, k - 1)

{{< / highlight >}}
</div>
</div>
