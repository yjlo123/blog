---
weight: 1597
title: "1597 Build Binary Expression Tree From Infix Expression"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_tree"]
---

A [binary expression tree](https://en.wikipedia.org/wiki/Binary_expression_tree) is a kind of binary tree used to represent arithmetic expressions. Each node of a binary expression tree has either zero or two children. Leaf nodes (nodes with 0 children) correspond to operands (numbers), and internal nodes (nodes with 2 children) correspond to the operators `'+'` (addition), `'-'` (subtraction), `'*'` (multiplication), and `'/'` (division).

For each internal node with operator `o`, the [infix expression](https://en.wikipedia.org/wiki/Infix_notation) it represents is `(A o B)`, where `A` is the expression the left subtree represents and `B` is the expression the right subtree represents.

You are given a string `s`, an **infix expression** containing operands, the operators described above, and parentheses `'('` and `')'`.

Return _any valid **binary expression tree**, whose [in-order traversal](https://en.wikipedia.org/wiki/Tree_traversal#In-order_(LNR)) reproduces s after omitting the parenthesis from it._

**Please note that order of operations applies in** `s`. That is, expressions in parentheses are evaluated first, and multiplication and division happen before addition and subtraction.

Operands must also appear in the **same order** in both `s` and the in-order traversal of the tree.

**Example 1:**
```
      -
     / \
   /     \
  *       *
 / \     / \
3   4   2   5

Input: s = "3*4-2*5"
Output: [-,*,*,3,4,2,5]
Explanation: The tree above is the only valid tree whose inorder traversal
produces s.
```
**Example 2:**
```
    +
   / \
  -   1
 / \
2   /
   / \
  3   *
     / \
    5   2

Input: s = "2-3/(5*2)+1"
Output: [+,-,1,2,/,null,null,null,null,3,*,null,null,5,2]
Explanation:
The inorder traversal of the tree above is 2-3/5*2+1 which is the same
as s without the parenthesis. The tree also produces the correct result and its
operands are in the same order as they appear in s.

The tree below is also a valid binary expression tree with the same inorder
traversal as s, but it not a valid answer because it does not evaluate to the
same value.

The third tree below is also not valid. Although it produces the same result and
is equivalent to the above trees, its inorder traversal does not produce s and its
operands are not in the same order as s.
```
**Example 3:**
```
Input: s = "1+2+3+4+5"
Output: [+,+,5,+,4,null,null,+,3,null,null,1,2]
Explanation: The tree [+,+,5,+,+,null,null,1,2,3,4] is also one of many
other valid trees.
```

**Constraints:**
- `1 <= s.length <= 100`
- `s` consists of digits and the characters `'+'`, `'-'`, `'*'`, and `'/'`.
- Operands in `s` are **exactly** 1 digit.
- It is guaranteed that `s` is a valid expression.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for a binary tree node.
# class Node(object):
#     def __init__(self, val=" ", left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # BNF:
    #   s := expression
    #   expression := term | term { [+,-] term] }
    #   term := factor | factor { [*,/] factor] }
    #   factor :== digit | '(' expression ')'
    #   digit := [0..9]
    
    def expTree(self, s: str) -> 'Node':
        tokens = collections.deque(list(s))
        return self.parse_expression(tokens)

    def parse_expression(self, tokens):
        lhs = self.parse_term(tokens)
        while len(tokens) > 0 and tokens[0] in ['+', '-']:
            op = tokens.popleft()
            rhs = self.parse_term(tokens)
            lhs = Node(val=op, left=lhs, right=rhs)
        return lhs
    
    def parse_term(self, tokens):
        lhs = self.parse_factor(tokens)
        while len(tokens) > 0 and tokens[0] in ['*', '/']:
            op = tokens.popleft()
            rhs = self.parse_factor(tokens)
            lhs = Node(val=op, left=lhs, right=rhs)
        return lhs

    def parse_factor(self, tokens):
        if tokens[0] == '(':
            tokens.popleft() # consume '('
            node = self.parse_expression(tokens)
            tokens.popleft() # consume ')'
            return node
        else:
            # Single operand
            token = tokens.popleft()
            return Node(val=token)
{{< / highlight >}}
</div>
</div>
