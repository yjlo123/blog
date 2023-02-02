---
weight: 1363
title: "1363 Largest Multiple of Three"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp", "lc_math"]
---

Given an array of digits `digits`, return *the largest multiple of **three** that can be formed by concatenating some of the given digits in **any order***. If there is no answer return an empty string.

Since the answer may not fit in an integer data type, return the answer as a string. Note that the returning answer must not contain unnecessary leading zeros.

**Example 1:**
```
Input: digits = [8,1,9]
Output: "981"
```
**Example 2:**
```
Input: digits = [8,6,7,1,0]
Output: "8760"
```
**Example 3:**
```
Input: digits = [1]
Output: ""
```

**Constraints:**
- <code>1 <= digits.length <= 10<sup>4</sup></code>
- `0 <= digits[i] <= 9`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def largestMultipleOfThree(self, digits: List[int]) -> str:
        total = sum(digits)
        count = collections.Counter(digits)
        digits.sort(reverse=True)

        def f(i):
            if count[i]:
                digits.remove(i)
                count[i] -= 1
            if not digits:
                return ''
            if not any(digits):
                return '0'
            if sum(digits) % 3 == 0:
                return ''.join(map(str, digits))

        '''
        If total % 3 == 0, done
        If total % 3 == 1 and there is one of 1,4,7 in digits:
            try to remove one of 1,4,7
        If total % 3 == 2 and we have one of 2,5,8 in digits:
            try to remove one of 2,5,8
        If total % 3 == 2:
            try to remove two of 1,4,7
        If total % 3 == 1:
            try to remove two of 2,5,8
        '''

        if total % 3 == 0:
            return f(-1)
        if total % 3 == 1 and count[1] + count[4] + count[7]:
            return f(1) or f(4) or f(7)
        if total % 3 == 2 and count[2] + count[5] + count[8]:
            return f(2) or f(5) or f(8)
        if total % 3 == 2:
            return f(1) or f(1) or f(4) or f(4) or f(7) or f(7)

        return f(2) or f(2) or f(5) or f(5) or f(8) or f(8)


'''
DP
'''
class Solution:
    def largestMultipleOfThree(self, digits: List[int]) -> str:
        # dp[i] is the largest number which dp[i] % 3 = i
        dp = [-1, -1, -1]
        for a in sorted(digits, reverse=True):
            for x in dp[:] + [0]:
                y = x * 10 + a
                dp[y % 3] = max(dp[y % 3], y)
        return str(dp[0]) if dp[0] >= 0 else ""
{{< / highlight >}}
</div>
</div>
