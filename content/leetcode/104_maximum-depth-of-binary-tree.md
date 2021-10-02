---
weight: 104
title: "104 Maximum Depth of Binary Tree"
date: 2021-10-02T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**
```
  3
 / \
9  20
   / \
  15  7

Input: root = [3,9,20,null,null,15,7]
Output: 3
```

**Example 2:**
```
Input: root = [1,null,2]
Output: 2
```

**Example 3:**
```
Input: root = []
Output: 0
```

**Example 4:**
```
Input: root = [0]
Output: 1
```

**Constraints:**
- The number of nodes in the tree is in the range [0, 10<sup>4</sup>].
- -100 <= `Node.val` <= 100

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
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
{{< / highlight >}}
</div>
</div>
