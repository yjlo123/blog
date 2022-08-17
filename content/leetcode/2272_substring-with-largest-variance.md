---
weight: 2272
title: "2272 Substring With Largest Variance"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard"]
---

The **variance** of a string is defined as the largest difference between the number of occurrences of **any** `2` characters present in the string. Note the two characters may or may not be the same.

Given a string s consisting of lowercase English letters only, return the _**largest variance** possible among all **substrings** of_ `s`.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**
```
Input: s = "aababbb"
Output: 3
Explanation:
All possible variances along with their respective substrings are listed below:
- Variance 0 for substrings "a", "aa", "ab", "abab", "aababb", "ba", "b", "bb", and "bbb".
- Variance 1 for substrings "aab", "aba", "abb", "aabab", "ababb", "aababbb", and "bab".
- Variance 2 for substrings "aaba", "ababbb", "abbb", and "babb".
- Variance 3 for substring "babbb".
Since the largest possible variance is 3, we return it.
```
**Example 2:**
```
Input: s = "abcde"
Output: 0
Explanation:
No letter occurs more than once in s, so the variance of every substring is 0.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>4</sup></code>
- `s` consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def largestVariance(self, s: str) -> int:
        chars = set(s)
        ans = 0
        for a in chars:
            for b in chars:
                diff = 0
                # max and min of diff
				# result should be max(diff - min_diff, max_diff - diff)
				# e.g. "baabaa"
                #      at index = 0, min_diff = -1
                #      when index = 5, diff = 4 - 2 = 2
                #      result = diff - min_diff = 2 - (-1) = 3
                max_diff = min_diff = 0
                last_a_diff = last_b_diff = 0
                meet_a = meet_b = False
                for c in s:
                    if c == a:
                        meet_a = True
                        diff += 1
                        max_diff = max(last_a_diff, max_diff)
                        last_a_diff = diff
                    elif c == b:
                        meet_b = True
                        diff -= 1
                        min_diff = min(last_b_diff, min_diff)
                        last_b_diff = diff
                    else:
                        continue
                    if meet_a and meet_b:
                        ans = max(
                            diff - min_diff,
                            max_diff - diff,
                            ans,
                        )
        return ans
{{< / highlight >}}
</div>
</div>
