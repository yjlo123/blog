---
weight: 557
title: "557 Reverse Words in a String III"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

Given a string `s`, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**
```
Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

**Example 2:**
```
Input: s = "God Ding"
Output: "doG gniD"
```

**Constraints:**
- 1 <= s.length <= 5 * 10<sup>4</sup>
- `s` contains printable **ASCII** characters.
- `s` does not contain any leading or trailing spaces.
- There is **at least one** word in `s`.
- All the words in `s` are separated by a single space.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def reverseWords(self, s: str) -> str:
        return ' '.join([w[::-1] for w in s.split(' ')])
{{< / highlight >}}
</div>
</div>
