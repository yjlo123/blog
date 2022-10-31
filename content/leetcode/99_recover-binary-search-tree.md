---
weight: 99
title: "99 Recover Binary Search Tree"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

You are given the `root` of a binary search tree (BST), where the values of **exactly** two nodes of the tree were swapped by mistake. _Recover the tree without changing its structure._

**Example 1:**
```
  (1)             3
  /              /
(3)      =>     1
  \              \
   2              2

Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1.
Swapping 1 and 3 makes the BST valid.
```

**Example 2:**
```
   (3)          2
   / \         / \
 1    4   =>  1   4
     /           /
   (2)          3

Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3.
Swapping 2 and 3 makes the BST valid.
```

**Constraints:**
- The number of nodes in the tree is in the range `[2, 1000]`.
- <code>-2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1</code>
 

**Follow up:** A solution using `O(n)` space is pretty straight-forward. Could you devise a constant `O(1)` space solution?

> Inorder traverse the BST, which supposed to generate an increasing array, record the two numbers that violate `A[i] < A[i+1]`.

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
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        self.first = None
        self.second = None
        self.prev = TreeNode(val=float('-inf'))
        self.inorder(root)
        self.first.val, self.second.val = self.second.val, self.first.val

    def inorder(self, root: Optional[TreeNode]) -> None:
        if not root:
            return
        self.inorder(root.left)
        if self.prev.val > root.val:
            if not self.first:
                self.first = self.prev
            self.second = root
        self.prev = root
        self.inorder(root.right)
{{< / highlight >}}
</div>
</div>
