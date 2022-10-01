---
weight: 105
title: "105 Construct Binary Tree from Preorder and Inorder Traversal"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and inorder is the `inorder` traversal of the same tree, construct and return _the binary tree_.

**Example 1:**
```
  3
 / \
9   20
   /  \
  15   7

Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```
**Example 2:**
```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

**Constraints:**
- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` and `inorder` consist of **unique** values.
- Each value of `inorder` also appears in `preorder`.
- `preorder` is **guaranteed** to be the preorder traversal of the tree.
- `inorder` is **guaranteed** to be the inorder traversal of the tree.

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
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        n = len(preorder)
        inorder_index_map = {}
        for index, value in enumerate(inorder):
            inorder_index_map[value] = index
        
        def build(pre_l, pre_r, in_l, in_r) -> Optional[TreeNode]:
            if pre_l > pre_r:
                return None
            root_val = preorder[pre_l]
            root = TreeNode(root_val)
            idx = inorder_index_map[root_val]
            left_inorder_size = idx - in_l
            root.left = build(
                pre_l + 1,
                pre_l + left_inorder_size,
                in_l,
                idx - 1
            )
            root.right = build(
                pre_l + left_inorder_size + 1,
                pre_r,
                idx + 1,
                in_r
            )
            return root

        return build(0, n-1, 0, n-1)
{{< / highlight >}}
</div>
</div>
