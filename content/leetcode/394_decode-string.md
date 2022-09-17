---
weight: 394
title: "394 Decode String"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack"]
---

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**
```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"
```
**Example 2:**
```
Input: s = "3[a2[c]]"
Output: "accaccacc"
```
**Example 3:**
```
Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
```

**Constraints:**
- `1 <= s.length <= 30`
- `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
- `s` is guaranteed to be **a valid** input.
- All the integers in `s` are in the range `[1, 300]`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []
        cur_num, cur_str = 0, ''
        for c in s:
            if c == '[':
                stack.append((cur_str, cur_num))
                cur_num, cur_str = 0, ''
            elif c == ']':
                prev_str, num = stack.pop()
                cur_str = prev_str + cur_str * num
            elif c.isdigit():
                cur_num = cur_num * 10 + int(c)
            else:
                cur_str += c
        return cur_str
{{< / highlight >}}
</div>
</div>
