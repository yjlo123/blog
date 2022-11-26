---
weight: 451
title: "451 Sort Characters By Frequency"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", lc_hash_table]
---

Given a string `s`, sort it in **decreasing order** based on the **frequency** of the characters. The **frequency** of a character is the number of times it appears in the string.

Return _the sorted string. If there are multiple answers, return any of them_.

**Example 1:**
```
Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```
**Example 2:**
```
Input: s = "cccaaa"
Output: "aaaccc"
Explanation: Both 'c' and 'a' appear three times,
so both "cccaaa" and "aaaccc" are valid answers.
Note that "cacaca" is incorrect, as the same characters must be together.
```
**Example 3:**
```
Input: s = "Aabb"
Output: "bbAa"
Explanation: "bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

**Constraints:**
- <code>1 <= s.length <= 5 * 10<sup>5</sup></code>
- `s` consists of uppercase and lowercase English letters and digits.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def frequencySort(self, s: str) -> str:
        counts = defaultdict(int)
        for c in s:
            counts[c] += 1
        
        string_builder = []
        for c, n in sorted(counts.items(), key=lambda x: -x[1]):
            string_builder.append(c * n)
        return ''.join(string_builder)
{{< / highlight >}}
</div>
</div>
