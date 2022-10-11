---
weight: 968
title: "968 Binary Tree Cameras"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs", "lc_tree", "lc_greedy"]
---

You are given the `root` of a binary tree. We install cameras on the tree nodes where each camera at a node can monitor its parent, itself, and its immediate children.

Return _the minimum number of cameras needed to monitor all nodes of the tree_.


**Example 1:**
```
    o
   /
  C
 / \
o   o

Input: root = [0,0,null,0,0]
Output: 1
Explanation: One camera is enough to monitor all nodes if placed as shown.
```
**Example 2:**
```
      o
     /
    C
   /
  o
 /
C
 \
  o

Input: root = [0,0,null,0,null,0,null,null,0]
Output: 2
Explanation: At least two cameras are needed to monitor all nodes of the tree.
The above image shows one of the valid configurations of camera placement.
```

**Constraints:**
- The number of nodes in the tree is in the range `[1, 1000]`.
- `Node.val == 0`

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
    def minCameraCover(self, root: Optional[TreeNode]) -> int:
        self.ans = 0
        covered = {None}
        
        def dfs(
            cur: Optional[TreeNode],
            parent: Optional[TreeNode]=None
        ) -> None:
            if not cur:
                return
            dfs(cur.left, cur)
            dfs(cur.right, cur)
            if (
                # if a node has no parent and it is not covered,
                # we must place a camera here
                (not parent and cur not in covered)
                or
                # if a node has children that are not covered by a camera,
                # then we must place a camera here
                (cur.left not in covered or cur.right not in covered)
            ):
                self.ans += 1
                covered.update({cur, parent, cur.left, cur.right})
        
        dfs(root)
        return self.ans
{{< / highlight >}}
</div>
</div>
