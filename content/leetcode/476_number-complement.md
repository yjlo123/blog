---
weight: 476
title: "476 Number Complement"
date: 2020-12-10T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_bit"]
---

The **complement** of an integer is the integer you get when you flip all the `0`'s to `1`'s and all the `1`'s to `0`'s in its binary representation.
- For example, The integer `5` is `"101"` in binary and its **complement** is `"010"` which is the integer `2`.

Given an integer `num`, return _its complement_.

**Example 1:**
```
Input: num = 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits),
and its complement is 010. So you need to output 2.
```

**Example 2:**
```
Input: num = 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits),
and its complement is 0. So you need to output 0.
```

**Constraints:**
- <code>1 <= num < 2<sup>31</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findComplement(self, num: int) -> int:
        todo, bit = num, 1
        while todo:
            num = num ^ bit
            bit <<= 1
            todo >>= 1
        return num
}
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func findComplement(num int) int {
	result := 0
	power := 1
	for num > 0 {
		result += (num % 2 ^ 1) * power
		power <<= 1
		num >>= 1
	}
	return result
}
{{< / highlight >}}
</div>
</div>
