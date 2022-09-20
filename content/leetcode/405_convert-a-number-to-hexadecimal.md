---
weight: 405
title: "405 Convert a Number to Hexadecimal"
date: 2021-03-30T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy"]
---

Given an integer `num`, return _a string representing its hexadecimal representation_. For negative integers, [two’s complement](https://en.wikipedia.org/wiki/Two%27s_complement) method is used.

All the letters in the answer string should be lowercase characters, and there should not be any leading zeros in the answer except for the zero itself.

**Note:** You are not allowed to use any built-in library method to directly solve this problem.

**Example 1:**
```
Input: num = 26
Output: "1a"
```
**Example 2:**
```
Input: num = -1
Output: "ffffffff"
```

**Constraints:**
- <code>-2<sup>31</sup> <= num <= 2<sup>31</sup> - 1</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def toHex(self, num: int) -> str:
        if num == 0:
            return '0'
        d = '0123456789abcdef'
        res = ''
        for i in range(8):
            res = d[num % 16] + res
            num >>= 4
        return res.lstrip('0')
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func toHex(num int) string {
    // fix to 32-bit int
	num32 := int32(num)
	if num32 == 0 {
		return "0"
	}
	result := ""
	for num32 != 0 {
		digit := num32 & 0xf
		var digitChar string
		if digit > 9 {
			digitChar = string(digit - 10 + int32('a'))
		} else {
			digitChar = strconv.Itoa(int(digit))
		}
		result = digitChar + result
		// unsigned shift
		num32 = int32(uint32(num32) >> 4)
	}
	return result
}
{{< / highlight >}}
</div>
</div>
