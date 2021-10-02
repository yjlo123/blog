---
weight: 102
title: "102 Binary Tree Level Order Traversal"
date: 2021-10-02T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**
```
  3
 / \
9  20
   / \
  15  7

Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

**Example 2:**
```
Input: root = [1]
Output: [[1]]
```

**Example 3:**
```
Input: root = []
Output: []
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 2000]`.
- -1000 <= `Node.val` <= 1000

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
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        def traverse(root, level, result):
            if not root:
                return
            if level > len(result)-1:
                result.append([])
            result[level].append(root.val)
            traverse(root.left, level+1, result)
            traverse(root.right, level+1, result)
        result = []
        traverse(root, 0, result)
        return result
{{< / highlight >}}
</div>
</div>
