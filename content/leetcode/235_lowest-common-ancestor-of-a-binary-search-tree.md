---
weight: 235
title: "235 Lowest Common Ancestor of a Binary Search Tree"
date: 2021-10-02T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow a node to be **a descendant of itself**).”

**Example 1:**
```
      6
    /   \
   2     8
 /  \   /  \
0    4 7    9
    / \
   3   5

Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

**Example 2:**
```
      6
    /   \
   2     8
 /  \   /  \
0    4 7    9
    / \
   3   5

Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of
itself according to the LCA definition.
```

**Example 3:**
```
Input: root = [2,1], p = 2, q = 1
Output: 2
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[2, 10<sup>5</sup>]</code>.
- <code>-10<sup>9</sup> <= Node.val <= 10<sup>9</sup></code>
- All `Node.val` are unique.
- `p != q`
- `p` and `q` will exist in the BST.

<div class="tabs"></div>
<div class="tab-content">

<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(
      self,
      root: 'TreeNode',
      p: 'TreeNode',
      q: 'TreeNode'
    ) -> 'TreeNode':
        while (root.val - p.val) * (root.val - q.val) > 0:
            root = root.left if p.val < root.val else root.right
        return root
{{< / highlight >}}
</div>
</div>
