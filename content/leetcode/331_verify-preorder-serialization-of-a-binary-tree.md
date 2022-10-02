---
weight: 331
title: "331 Verify Preorder Serialization of a Binary Tree"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

One way to serialize a binary tree is to use **preorder traversal**. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as `'#'`.

```
    9
   / \
  3   2
 / \   \
4   1   6
```

For example, the above binary tree can be serialized to the string `"9,3,4,#,#,1,#,#,2,#,6,#,#"`, where `'#'` represents a null node.

Given a string of comma-separated values `preorder`, return `true` if it is a correct preorder traversal serialization of a binary tree.

It is guaranteed that each comma-separated value in the string must be either an integer or a character `'#'` representing null pointer.

You may assume that the input format is always valid.

- For example, it could never contain two consecutive commas, such as `"1,,3"`.

**Note:** You are not allowed to reconstruct the tree.

**Example 1:**
```
Input: preorder = "9,3,4,#,#,1,#,#,2,#,6,#,#"
Output: true
```
**Example 2:**
```
Input: preorder = "1,#"
Output: false
```
**Example 3:**
```
Input: preorder = "9,#,#,1"
Output: false
```

**Constraints:**
- <code>1 <= preorder.length <= 10<sup>4</sup></code>
- `preorder` consist of integers in the range `[0, 100]` and `'#'` separated by commas `','`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def isValidSerialization(self, preorder: str) -> bool:
        slots = 1
        for node in preorder.split(','):
            slots -= 1

            if slots < 0:
                return False

            if node != '#':
                slots += 2

        return slots == 0
{{< / highlight >}}
</div>
</div>
