---
weight: 314
title: "314 Binary Tree Vertical Order Traversal"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_bfs"]
---

Given the `root` of a binary tree, return _**the vertical order traversal** of its nodes' values._ (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from **left to right**.

**Example 1:**
```
  3
 / \
9   20
   /  \
  15   7

Input: root = [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
```
**Example 2:**
```
     3
    / \
  9     8
 / \   / \
4   0,1   7

Input: root = [3,9,8,4,0,1,7]
Output: [[4],[9],[3,0,1],[8],[7]]
```
**Example 3:**
```
     3
    / \
  9     8
 / \   / \
4   0,1   7
    \ /
    / \
  5     2

Input: root = [3,9,8,4,0,1,7,null,null,null,2,5]
Output: [[4],[9,5],[3,0,1],[8,2],[7]]
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

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
    def verticalOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        
        d = {}
        min_col = 0
        q = deque([(root, 0)])
        while q:
            node, col = q.popleft()
            min_col = min(min_col, col)
            d.setdefault(col, []).append(node.val)
            if node.left:  
                q.append((node.left, col - 1))
            if node.right:
                q.append((node.right, col + 1))
        
        res = []
        cur_col = min_col
        while cur_col in d:
            res.append(d[cur_col])
            cur_col += 1
        return res
{{< / highlight >}}
</div>
</div>
