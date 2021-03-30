---
weight: 405
title: "405 Convert a Number to Hexadecimal"
date: 2021-03-30T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy"]
---

Given an integer, write an algorithm to convert it to hexadecimal. For negative integer, `two’s complement` method is used.

Note:

All letters in hexadecimal (`a-f`) must be in lowercase.
The hexadecimal string must not contain extra leading 0s. If the number is zero, it is represented by a single zero character `'0'`; otherwise, the first character in the hexadecimal string will not be the zero character.
The given number is guaranteed to fit within the range of a 32-bit signed integer.
You **must not use _any_ method provided by the library** which converts/formats the number to hex directly.
**Example 1:**
```
Input:
26

Output:
"1a"
```
**Example 2:**
```
Input:
-1

Output:
"ffffffff"
```

<div class="tabs"></div>
<div class="tab-content">
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
