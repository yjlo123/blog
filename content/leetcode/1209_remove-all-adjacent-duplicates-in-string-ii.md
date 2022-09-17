---
weight: 1209
title: "1209 Remove All Adjacent Duplicates in String II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string", "lc_stack"]
---

You are given a string `s` and an integer `k`, a `k` **duplicate removal** consists of choosing `k` adjacent and equal letters from `s` and removing them, causing the left and the right side of the deleted substring to concatenate together.

We repeatedly make `k` **duplicate removals** on `s` until we no longer can.

Return _the final string after all such duplicate removals have been made_. It is guaranteed that the answer is **unique**.

**Example 1:**
```
Input: s = "abcd", k = 2
Output: "abcd"
Explanation: There's nothing to delete.
```
**Example 2:**
```
Input: s = "deeedbbcccbdaa", k = 3
Output: "aa"
Explanation: 
First delete "eee" and "ccc", get "ddbbbdaa"
Then delete "bbb", get "dddaa"
Finally delete "ddd", get "aa"
```
**Example 3:**
```
Input: s = "pbbcggttciiippooaais", k = 2
Output: "ps"
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- <code>2 <= k <= 10<sup>4</sup></code>
- `s` only contains lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        stack = []  # [count, char]
        for c in s:
            if not stack or c != stack[-1][1]:
                stack.append([1, c])
            else:
                stack[-1][0] += 1
                if stack[-1][0] == k:
                    stack.pop()
        return ''.join([char * count for count, char in stack])
{{< / highlight >}}
</div>
</div>
