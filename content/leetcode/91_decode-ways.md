---
weight: 91
title: "91 Decode Ways"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:
```
'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
```
To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:

- `"AAJF"` with the grouping `(1 1 10 6)`
- `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return _the **number** of ways to **decode** it._

The test cases are generated so that the answer fits in a **32-bit** integer.

**Example 1:**
```
Input: s = "12"
Output: 2
Explanation: "12" could be decoded as "AB" (1 2) or "L" (12).
```
**Example 2:**
```
Input: s = "226"
Output: 3
Explanation: "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```
**Example 3:**
```
Input: s = "06"
Output: 0
Explanation: "06" cannot be mapped to "F" because of the leading zero
("6" is different from "06").
```

**Constraints:**
- `1 <= s.length <= 100`
- `s` contains only digits and may contain leading zero(s).

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numDecodings(self, s: str) -> int:
        dp = [0] * len(s)
        if s[0] == '0':
            return 0
        dp[0] = 1
        for i in range(1, len(s)):
            c = s[i]
            if c.isdigit() and 0 < int(c) < 27:
                dp[i] += dp[i-1]
            if 9 < int(s[i-1:i+1]) < 27:
                dp[i] += dp[i-2] if i > 1 else 1
            if dp[i] == 0:
                return 0
        return dp[-1]
{{< / highlight >}}
</div>
</div>
