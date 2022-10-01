---
weight: 98
title: "98 Validate Binary Search Tree"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_bst"]
---

Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:
- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**
```
  2
 / \
1   3

Input: root = [2,1,3]
Output: true
```
**Example 2:**
```
  5
 / \
1   4
   / \
  3   6

Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.
- <code>-2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1</code>

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
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def validate(
            node: Optional[TreeNode],
            low=-math.inf,
            high=math.inf
        ) -> bool:
            if not node:
                return True
            if node.val <= low or node.val >= high:
                return False
            return (
                validate(node.left, low, node.val) and
                validate(node.right, node.val, high)
            )

        return validate(root)

'''
In order
'''
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:

        def inorder(root):
            if not root:
                return True
            if not inorder(root.left):
                return False
            if root.val <= self.prev:
                return False
            self.prev = root.val
            return inorder(root.right)

        self.prev = -math.inf
        return inorder(root)
{{< / highlight >}}
</div>
</div>
