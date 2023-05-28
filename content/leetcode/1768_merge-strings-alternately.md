---
weight: 1768
title: "1768 Merge Strings Alternately"
date: 2023-05-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

You are given two strings `word1` and `word2`. Merge the strings by adding letters in alternating order, starting with `word1`. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return *the merged string*.

**Example 1:**
```
Input: word1 = "abc", word2 = "pqr"
Output: "apbqcr"
Explanation: The merged string will be merged as so:
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
```
**Example 2:**
```
Input: word1 = "ab", word2 = "pqrs"
Output: "apbqrs"
Explanation: Notice that as word2 is longer, "rs" is appended to the end.
word1:  a   b 
word2:    p   q   r   s
merged: a p b q   r   s
```
**Example 3:**
```
Input: word1 = "abcd", word2 = "pq"
Output: "apbqcd"
Explanation: Notice that as word1 is longer, "cd" is appended to the end.
word1:  a   b   c   d
word2:    p   q 
merged: a p b q c   d
```

**Constraints:**
- `1 <= word1.length, word2.length <= 100`
- `word1` and `word2` consist of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        n1, n2 = len(word1), len(word2)
        res = []
        for i in range(max(n1, n2)):
            if i < n1:
                res.append(word1[i])
            if i < n2:
                res.append(word2[i])
        return ''.join(res)
{{< / highlight >}}
</div>
<div id="golang" class="lang">
{{< highlight golang "linenos=table" >}}
func mergeAlternately(word1 string, word2 string) string {
    var res []byte
    for i := 0; i < len(word1) || i < len(word2); i++ {
        if i < len(word1) {
            res = append(res, word1[i])
        }
        if i < len(word2) {
            res = append(res, word2[i])
        }
    }
    return string(res)
}
{{< / highlight >}}
</div>
</div>
