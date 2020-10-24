---
weight: 5
title: "5 Longest Palindromic Substring"
date: 2020-09-23T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

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
</div>
