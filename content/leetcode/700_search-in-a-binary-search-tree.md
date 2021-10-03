---
weight: 700
title: "700 Search in a Binary Search Tree"
date: 2021-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

You are given the `root` of a binary search tree (BST) and an integer `val`.

Find the node in the BST that the node's value equals `val` and return the subtree rooted with that node. If such a node does not exist, return `null`.

**Example 1:**
```
      4
     / \
   (2)  7
  /  \
(1)  (3)

Input: root = [4,2,7,1,3], val = 2
Output: [2,1,3]
```

**Example 2:**
```
     4
    / \
   2   7
  / \
 1   3

Input: root = [4,2,7,1,3], val = 5
Output: []
```

**Constraints:**
- The number of nodes in the tree is in the range `[1, 5000]`.
- 1 <= `Node.val` <= 10<sup>7</sup>
- `root` is a binary search tree.
- 1 <= `val` <= 10<sup>7</sup>

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
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        if root is None or root.val == val:
            return root
        if root.val > val:
            return self.searchBST(root.left, val)
        return self.searchBST(root.right, val)

{{< / highlight >}}
</div>
</div>
