---
weight: 250
title: "250 Count Univalue Subtrees"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the `root` of a binary tree, return _the number of **uni-value** subtrees (A subtree of treeName is a tree consisting of a node in treeName and all of its descendants)._

A **uni-value subtree** means all nodes of the subtree have the same value.


**Example 1:**
```
     5
    / \
   1  (5)
  / \   \
(5) (5) (5)

Input: root = [5,1,5,5,5,null,5]
Output: 4
```
**Example 2:**
```
Input: root = []
Output: 0
```
**Example 3:**
```
Input: root = [5,5,5,5,5,null,5]
Output: 6
```

**Constraints:**
- The number of the node in the tree will be in the range `[0, 1000]`.
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
    def is_valid_part(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True
        
        if root.left == root.right:
            # leaf
            self.total += 1
            return True

        result = True
        if root.left:
            left_all_same = self.is_valid_part(root.left)
            if not left_all_same or root.val != root.left.val:
                result = False
        if root.right:
            right_all_same = self.is_valid_part(root.right)
            if not right_all_same or root.val != root.right.val:
                result = False
        if result:
            self.total += 1
        return result

    def countUnivalSubtrees(self, root: Optional[TreeNode]) -> int:
        self.total = 0
        self.is_valid_part(root)
        return self.total


'''
Shorter
'''
class Solution:
    def is_valid_part(
        self,
        node: Optional[TreeNode],
        parent_val: int
    ) -> bool:
        if not node:
            return True

        is_left_valid = self.is_valid_part(node.left, node.val)
        is_right_valid = self.is_valid_part(node.right, node.val)
        # be careful of Short-Circuit Evaluation
        if not is_left_valid or not is_right_valid:
            return False
        self.count += 1
        return node.val == parent_val

    def countUnivalSubtrees(self, root: Optional[TreeNode]) -> int:
        self.count = 0
        self.is_valid_part(root, 0)
        return self.count
{{< / highlight >}}
</div>
</div>
