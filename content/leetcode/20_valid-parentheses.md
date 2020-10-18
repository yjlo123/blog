---
weight: 20
title: "20 Valid Parentheses"
date: 2020-09-25T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

**Example 1:**
```
Input: s = "()"
Output: true
```

**Example 2:**
```
Input: s = "()[]{}"
Output: true
```

**Example 3:**
```
Input: s = "(]"
Output: false
```

**Example 4:**
```
Input: s = "([)]"
Output: false
```

**Example 5:**
```
Input: s = "{[]}"
Output: true
```

**Constraints:**

- 1 <= s.length <= 10<sup>4</sup>
- `s` consists of parentheses only `'()[]{}'`.

<div class="tabs">
  <div class="tab-btn tab-btn-active" onclick="showLang(event, 'golang')">Golang</div>
  <div class="tab-btn" onclick="showLang(event, 'runtime')">Runtime</div>
</div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
import (
    "fmt"
)

func isValid(s string) bool {
    var stack []byte

    for i := 0; i < len(s); i++ {
        c := s[i]
        if c == '(' || c == '[' || c == '{' {
            stack = append(stack, c)
        } else if c == ')' && len(stack) > 0 && stack[len(stack)-1] == '(' {
            stack = stack[:len(stack)-1]
        } else if c == ']' && len(stack) > 0 && stack[len(stack)-1] == '[' {
            stack = stack[:len(stack)-1]
        } else if c == '}' && len(stack) > 0 && stack[len(stack)-1] == '{' {
            stack = stack[:len(stack)-1]
        } else {
            return false
        }
    }
    return true
}

func main() {
    fmt.Println(isValid("{[()]}"))
}
{{< / highlight >}}
</div>
<div id="runtime" class="lang" style="display:none">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode20" target="_blank">https://runtime.siwei.dev/?src=leetcode20</a>
    </div>
</div>
</div>
