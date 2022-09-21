---
weight: 124
title: "124 Binary Tree Maximum Path Sum"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_tree"]
---

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return the _maximum **path sum** of any **non-empty** path_.

**Example 1:**
```
   1
  / \
 2   3

Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```
**Example 2:**
```
 -10
 / \
9   20
   /  \
  15   7

Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[1, 3 * 10<sup>4</sup>]</code>.
- `-1000 <= Node.val <= 1000`

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
    def __init__(self):
        self.max_sum = float('-inf')
        
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        self.traverse(root)
        return self.max_sum
    
    def traverse(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        left = self.traverse(root.left)
        right = self.traverse(root.right)
        self.max_sum = max(self.max_sum, left + right + root.val)
        return max(max(left, right) + root.val, 0)
{{< / highlight >}}
</div>
</div>
