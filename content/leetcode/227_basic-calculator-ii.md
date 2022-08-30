---
weight: 227
title: "227 Basic Calculator II"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack", "lc_math"]
---

Given a string `s` which represents an expression, _evaluate this expression and return its value._

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>.

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**
```
Input: s = "3+2*2"
Output: 7
```
**Example 2:**
```
Input: s = " 3/2 "
Output: 1
```
**Example 3:**
```
Input: s = " 3+5 / 2 "
Output: 5
```

**Constraints:**
- <code>1 <= s.length <= 3 * 10<sup>5</sup></code>
- `s` consists of integers and operators `('+', '-', '*', '/')` separated by some number of spaces.
- `s` represents **a valid expression**.
- All the integers in the expression are non-negative integers in the range <code>[0, 2<sup>31</sup> - 1]</code>.
- The answer is **guaranteed** to fit in a **32-bit integer**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    PRECEDENCE = {
        '*': 2,
        '/': 2,
        '+': 1,
        '-': 1,
    }
    
    OPS = {
        '+': lambda x, y: x + y,
        '-': lambda x, y: x - y,
        '*': lambda x, y: x * y,
        '/': lambda x, y: x // y,
    }
    
    def calculate(self, s: str) -> int:
        # tokenize
        tokens = []
        token = ""
        for c in s:
            if c in self.PRECEDENCE:
                if token:
                    tokens.append(int(token))
                    token = ''
                tokens.append(c)
            else:
                token += c
        if token:
            tokens.append(int(token))
        
        # in-order to post-order
        stack = []
        post_tokens = []
        for t in tokens:
            if t in self.PRECEDENCE:
                while stack and self.PRECEDENCE[stack[-1]] >= self.PRECEDENCE[t]:
                    post_tokens.append(stack.pop())
                stack.append(t)
                continue
            post_tokens.append(t)
        while stack:
            post_tokens.append(stack.pop())
        
        # evaluate
        stack = []
        for t in post_tokens:
            if t in self.PRECEDENCE:
                operand_2 = stack.pop()
                operand_1 = stack.pop()
                stack.append(self.OPS[t](operand_1, operand_2))
            else:
                stack.append(t)
        return stack[0]


'''
Shorter Version (without using stacks)
'''
class Solution:
    def calculate(self, s: str) -> int:
        if len(s) == 0:
            return 0
        current_num = 0
        last_num = 0
        result = 0
        op = '+'
        for i, c in enumerate(s):
            if c.isdigit():
                current_num = current_num * 10 + int(c)
            if not c.isdigit() and c != ' ' or i == len(s)-1:
                if op in '+-':
                    result += last_num
                    last_num = current_num if op == '+' else -current_num
                elif op == '*':
                    last_num *= current_num
                elif op == '/':
                    last_num = int(last_num/current_num)
                op = c
                current_num = 0
        result += last_num
        return result
{{< / highlight >}}
</div>
</div>
