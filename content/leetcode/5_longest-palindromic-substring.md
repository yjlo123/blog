---
weight: 5
title: "5 Longest Palindromic Substring"
date: 2020-09-23T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

Given a string `s`, return _the longest palindromic substring in `s`_.

**Example1:**
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
**Example2:**
```
Input: "cbbd"
Output: "bb"
```

**Constraints:**
- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func longestPalindrome(s string) string {
    if len(s) < 1 {
        return ""
    }
    start := 0
    end := 0
    for i := range s {
        len1 := expandAroundCenter(s, i, i)
        len2 := expandAroundCenter(s, i, i+1)
        lenMax := -1
        if len1 > len2 {
            lenMax = len1
        } else {
            lenMax = len2
        }

        if lenMax > end-start+1 {
            start = i - (lenMax-1)/2
            end = i + lenMax/2
        }
    }
    return s[start : end+1]
}

func expandAroundCenter(s string, left int, right int) int {
    for left >= 0 && right < len(s) && s[left] == s[right] {
        left--
        right++
    }
    return right - left - 1
}
{{< / highlight >}}
</div>
<div id="runtime" class="lang">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode5" target="_blank">https://runtime.siwei.dev/?src=leetcode5</a>
    </div>
</div>
</div>
