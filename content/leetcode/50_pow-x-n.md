---
weight: 50
title: "50 Pow(x, n)"
date: 2021-03-11T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium"]
---

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e. <code>x<sup>n</sup></code>).

**Example 1:**
```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

**Example 2:**
```
Input: x = 2.10000, n = 3
Output: 9.26100
```

**Example 3:**
```
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2^(-2) = 1/(2^2) = 1/4 = 0.25
 ```

**Constraints:**

- `-100.0 < x < 100.0`
- <code>-2<sup>31</sup> <= n <= 2<sup>31</sup>-1</code>
- <code>-10<sup>4</sup> <= x<sup>n</sup> <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        if n < 0:
            return self.myPow(1 / x, -n)
        res = self.myPow(x * x, n // 2)
        if n % 2 == 1:
            res *= x
        return res
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func myPow(x float64, n int) float64 {
    if n == 0 {
        return 1
    }
    if n < 0 {
        return myPow(1/x, -n)
    }
    result := myPow(x*x, n/2)
    if n % 2 == 1 {
        result *= x
    }
    return result
}
{{< / highlight >}}
</div>
</div>
