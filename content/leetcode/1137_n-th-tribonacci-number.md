---
weight: 1137
title: "1137 N-th Tribonacci Number"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_dp"]
---

The Tribonacci sequence Tn is defined as follows: 

T<sub>0</sub> = 0, T<sub>1</sub> = 1, T<sub>2</sub> = 1, and T<sub>n+3</sub> = T<sub>n</sub> + T<sub>n+1</sub> + T<sub>n+2</sub> for n >= 0.

Given n, return the value of T<sub>n</sub>.

**Example 1:**
```
Input: n = 4
Output: 4
Explanation:
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```
**Example 2:**
```
Input: n = 25
Output: 1389537
```

**Constraints:**
- `0 <= n <= 37`
- The answer is guaranteed to fit within a 32-bit integer, ie. `answer <= 2^31 - 1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def __init__(self):
        n = 38
        self.nums = [0] * n
        self.nums[1] = self.nums[2] = 1
        def trib(k):
            if k == 0:
                return 0
            if self.nums[k]:
                return self.nums[k]
            self.nums[k] = trib(k-1) + trib(k-2) + trib(k-3)
            return self.nums[k]
        trib(n-1)
            
    
    def tribonacci(self, n: int) -> int:
        return self.nums[n]
{{< / highlight >}}
</div>
</div>
