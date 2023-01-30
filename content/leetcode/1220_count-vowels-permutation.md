---
weight: 1220
title: "1220 Count Vowels Permutation"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp"]
---

Given an integer `n`, your task is to count how many strings of length `n` can be formed under the following rules:

Each character is a lower case vowel (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`)
Each vowel `'a'` may only be followed by an `'e'`.
Each vowel `'e'` may only be followed by an `'a'` or an `'i'`.
Each vowel `'i'` may not be followed by another `'i'`.
Each vowel `'o'` may only be followed by an `'i'` or a `'u'`.
Each vowel `'u'` may only be followed by an `'a'`.
Since the answer may be too large, return it modulo <code>10<sup>9</sup> + 7</code>.

**Example 1:**
```
Input: n = 1
Output: 5
Explanation: All possible strings are: "a", "e", "i" , "o" and "u".
```
**Example 2:**
```
Input: n = 2
Output: 10
Explanation: All possible strings are: "ae", "ea", "ei", "ia", "ie", "io", "iu", "oi", "ou" and "ua".
```
**Example 3:**
```
Input: n = 5
Output: 68
```

**Constraints:**
- <code>1 <= n <= 2 * 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def countVowelPermutation(self, n: int) -> int:
     a = e = i = o = u = 1
     mod = 10 ** 9 + 7
     for _ in range(2, n + 1):
         a, e, i, o, u = (
             (e + u + i) % mod,
             (a + i) % mod,
             (e + o) % mod,
             i,
             (o + i) % mod 
         )
     return sum([a, e, i, o, u]) % mod
{{< / highlight >}}
</div>
</div>
