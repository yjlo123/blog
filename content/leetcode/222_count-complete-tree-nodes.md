---
weight: 222
title: "222 Count Complete Tree Nodes"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the `root` of a **complete** binary tree, return the number of the nodes in the tree.

According to [Wikipedia](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees), every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between `1` and <code>2<sup>h</sup></code> nodes inclusive at the last level `h`.

Design an algorithm that runs in less than `O(n)` time complexity.

**Example 1:**
```
     1
   /   \
  2     3
 / \   /
4   5 6

Input: root = [1,2,3,4,5,6]
Output: 6
```
**Example 2:**
```
Input: root = []
Output: 0
```
**Example 3:**
```
Input: root = [1]
Output: 1
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.
- <code>0 <= Node.val <= 5 * 10<sup>4</sup></code>
- The tree is guaranteed to be **complete**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        # count the depth of left-most and right-most nodes
        l, r = root, root
        lh, rh = 0, 0
        while l:
            l = l.left
            lh += 1
        while r:
            r = r.right
            rh += 1

        # if left-most and right-most have the same depth
        # the current tree is a full binary tree
        if lh == rh:
            return 2 ** lh - 1
        return 1 + self.countNodes(root.left) + self.countNodes(root.right)

{{< / highlight >}}
</div>
</div>
