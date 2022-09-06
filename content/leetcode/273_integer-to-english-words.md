---
weight: 273
title: "273 Integer to English Words"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_math"]
---

Convert a non-negative integer `num` to its English words representation.

**Example 1:**
```
Input: num = 123
Output: "One Hundred Twenty Three"
```
**Example 2:**
```
Input: num = 12345
Output: "Twelve Thousand Three Hundred Forty Five"
```
**Example 3:**
```
Input: num = 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**Constraints:**
- <code>0 <= num <= 2<sup>31</sup> - 1</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberToWords(self, num: int) -> str:
        if not num:
            return 'Zero'
        ones = ['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine', 'Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen']
        tens = ['', 'Ten', 'Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety']
        thoudands = ['', 'Thousand', 'Million', 'Billion', 'Trillion']
        res = ''
        i = 0
        while num > 0:
            if num % 1000 > 0:
                res = ' ' + thoudands[i] + res
                current = ''
                third = num // 100 % 10
                second = num % 100
                first = num % 10
                if third:
                    current += (' ' + ones[third] + ' Hundred')
                if 0 < second < 20:
                    current += (' ' + ones[second])
                else:
                    if second:
                        current += (' ' + tens[second // 10])
                    if first:
                        current += (' ' + ones[first])
                res = current + res
            num //= 1000
            i += 1
        return res.strip()
{{< / highlight >}}
</div>
</div>
