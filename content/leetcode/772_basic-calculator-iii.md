---
weight: 772
title: "772 Basic Calculator III"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_stack", "lc_math"]
---

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, `'+'`, `'-'`, `'*'`, `'/'` operators, and open `'('` and closing parentheses `')'`. The integer division should **truncate toward zero**.

You may assume that the given expression is always valid. All intermediate results will be in the range of <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>.

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**
```
Input: s = "1+1"
Output: 2
```
**Example 2:**
```
Input: s = "6-4/2"
Output: 4
```
**Example 3:**
```
Input: s = "2*(5+5*2)/3+(6/2+8)"
Output: 21
```

**Constraints:**
- <code>1 <= s <= 10<sup>4</sup></code>
- `s` consists of digits, `'+'`, `'-'`, `'*'`, `'/'`, `'('`, and `')'`.
- `s` is a **valid** expression.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    def calculate(self, s: str) -> int:
        def calc(s: List) -> int:
            stack = []
            sign = '+'
            num = 0

            while len(s) > 0:
                c = s.popleft()
                if c.isdigit():
                    num = 10 * num + int(c)
                if c == '(':
                    num = calc(s)

                if (not c.isdigit() and c != ' ') or len(s) == 0:
                    if sign == '+':
                        stack.append(num)
                    elif sign == '-':
                        stack.append(-num)
                    elif sign == '*':
                        stack[-1] = stack[-1] * num
                    elif sign == '/':
                        stack[-1] = int(stack[-1] / float(num))       
                    num = 0
                    sign = c
                if c == ')':
                    break
            return sum(stack)

        return calc(collections.deque(s))
{{< / highlight >}}
</div>
</div>
