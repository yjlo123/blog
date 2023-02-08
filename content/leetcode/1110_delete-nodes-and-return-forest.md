---
weight: 1110
title: "1110 Delete Nodes And Return Forest"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the `root` of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in `to_delete`, we are left with a forest (a disjoint union of trees).

Return *the roots of the trees in the remaining forest*. You may return the result in any order.

**Example 1:**
```
      1
     / \
   /     \
  2       3
 / \     / \
4   5   6   7

Input: root = [1,2,3,4,5,6,7], to_delete = [3,5]
Output: [[1,2,null,4],[6],[7]]
```
**Example 2:**
```
Input: root = [1,2,4,null,3], to_delete = [3]
Output: [[1,2,4]]
```

**Constraints:**
- The number of nodes in the given tree is at most `1000`.
- Each node has a distinct value between `1` and `1000`.
- `to_delete.length <= 1000`
- `to_delete` contains distinct values between `1` and `1000`.

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
    def delNodes(self, root: Optional[TreeNode], to_delete: List[int]) -> List[TreeNode]:
        to_del = set(to_delete)
        res = []

        def helper(node, is_root):
            if not node:
                return None

            root_deleted = node.val in to_del
            if is_root and not root_deleted:
                res.append(node)

            node.left = helper(node.left, root_deleted)
            node.right = helper(node.right, root_deleted)
            return None if root_deleted else node

        helper(root, True)
        return res
{{< / highlight >}}
</div>
</div>
