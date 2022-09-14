---
weight: 2222
title: "2222 Number of Ways to Select Buildings"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp", "lc_string"]
---

You are given a **0-indexed** binary string `s` which represents the types of buildings along a street where:
- `s[i] = '0'` denotes that the <code>i<sup>th</sup></code> building is an office and
- `s[i] = '1'` denotes that the <code>i<sup>th</sup></code> building is a restaurant.

As a city official, you would like to **select** 3 buildings for random inspection. However, to ensure variety, **no two consecutive** buildings out of the **selected** buildings can be of the same type.

- For example, given `s = "001101"`, we cannot select the <code>1<sup>st</sup></code>, <code>3<sup>rd</sup></code>, and <code>5<sup>th</sup></code> buildings as that would form `"011"` which is **not** allowed due to having two consecutive buildings of the same type.

Return _the **number of valid ways** to select 3 buildings_.

**Example 1:**
```
Input: s = "001101"
Output: 6
Explanation: 
The following sets of indices selected are valid:
- [0,2,4] from "001101" forms "010"
- [0,3,4] from "001101" forms "010"
- [1,2,4] from "001101" forms "010"
- [1,3,4] from "001101" forms "010"
- [2,4,5] from "001101" forms "101"
- [3,4,5] from "001101" forms "101"
No other selection is valid. Thus, there are 6 total ways.
```
**Example 2:**
```
Input: s = "11100"
Output: 0
Explanation: It can be shown that there are no valid selections.
```

**Constraints:**
- <code>3 <= s.length <= 10<sup>5</sup></code>
- `s[i]` is either `'0'` or `'1'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberOfWays(self, s: str) -> int:
        ways = 0
        one = zero = zero_one = one_zero = 0
        for c in s:
            if c == '0':
                zero += 1
                # '1' + '0' => '10'
                one_zero += one
                # '01' + '0' => '010'
                ways += zero_one
            else:
                one += 1    
                # '0' + '1' => '01'
                zero_one += zero
                # '10' + '1' => '101'
                ways += one_zero
        return ways
{{< / highlight >}}
</div>
</div>
