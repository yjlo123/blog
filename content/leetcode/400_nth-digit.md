---
weight: 400
title: "400 Nth Digit"
date: 2020-10-28T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium"]
---

Find the n<sup>th</sup> digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

**Note:**
_n_ is positive and will fit within the range of a 32-bit signed integer (n < 2<sup>31</sup>).

**Example 1:**
```
Input:
3

Output:
3
```
**Example 2:**
```
Input:
11

Output:
0

Explanation:
The 11th digit of the sequence
  1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...
  is a 0, which is part of the number 10.
```

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func findNthDigit(n int) int {
	length := 1
	rangeCount := 9
	num := 1
	for n > length*rangeCount {
		n -= length * rangeCount
		length += 1
		rangeCount *= 10
		num *= 10
	}
	num += (n - 1) / length
	return int(strconv.Itoa(num)[(n-1)%length] - '0')
}
{{< / highlight >}}
</div>
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
def findNthDigit(n: int) -> int:
    length = 1       # number of digits: 1, 2, 3 ...
    range_count = 9  # count of numbers for current length: 9, 90, 900 ...
    num = 1          # current number: 1, 10, 100, 1000 ...
    while n > length * range_count:
        n -= length * range_count
        length += 1
        range_count *= 10
        num *= 10
    num += (n-1) / length
    return int(str(num)[(n-1) % length])
{{< / highlight >}}
</div>
</div>
