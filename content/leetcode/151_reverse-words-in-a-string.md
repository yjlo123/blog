---
weight: 151
title: "151 Reverse Words in a String"
date: 2023-05-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string", "lc_array"]
---

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space*.

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1:**
```
Input: s = "the sky is blue"
Output: "blue is sky the"
```
**Example 2:**
```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```
**Example 3:**
```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>4</sup></code>
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is at **least one** word in `s`.

**Follow-up:** If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def reverseWords(self, s: str) -> str:
        return ' '.join(reversed(s.split()))
{{< / highlight >}}
</div>
<div id="golang" class="lang">
{{< highlight golang "linenos=table" >}}
func reverseWords(s string) string {
    words := strings.Fields(s)
    n := len(words)
    for i:=0; i < n/2; i++ {
        words[i], words[n-i-1] = words[n-i-1], words[i]
    }
    return strings.Join(words, " ")
}
{{< / highlight >}}
</div>
</div>
