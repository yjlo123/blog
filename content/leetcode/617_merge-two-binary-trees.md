---
weight: 617
title: "617 Merge Two Binary Trees"
date: 2021-09-23T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

You are given two binary trees `root1` and `root2`.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

Return _the merged tree_.

**Note**: The merging process must start from the root nodes of both trees.

**Example 1:**
```
     1         2               3
    / \       / \             / \
   3   2     1   3     =>    4   5
  /           \   \         / \   \
 5             4   7       5   4   7

Input: root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
Output: [3,4,5,5,4,null,7]
```

**Example 2:**
```
Input: root1 = [1], root2 = [1,2]
Output: [2,2]
```

**Constraints:**
- The number of nodes in both trees is in the range `[0, 2000]`.
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup>

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
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if root1 and root2:
            return TreeNode(
                root1.val+root2.val,
                self.mergeTrees(root1.left, root2.left),
                self.mergeTrees(root1.right, root2.right)
            )
        return root1 or root2
{{< / highlight >}}
</div>
</div>
