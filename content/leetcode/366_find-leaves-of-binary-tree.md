---
weight: 366
title: "366 Find Leaves of Binary Tree"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_dfs"]
---

Given the `root` of a binary tree, collect a tree's nodes as if you were doing this:
- Collect all the leaf nodes.
- Remove all the leaf nodes.
- Repeat until the tree is empty.

**Example 1:**
```
    1
   / \          1
  2   3   =>   /    =>   1
 / \          2
4   5

Input: root = [1,2,3,4,5]
Output: [[4,5,3],[2],[1]]
Explanation:
[[3,5,4],[2],[1]] and [[3,4,5],[2],[1]] are also considered correct answers
since per each level it does not matter the order on which elements are returned.
```
**Example 2:**
```
Input: root = [1]
Output: [[1]]
```

**Constraints:**
- The number of nodes in the tree is in the range `[1, 100]`.
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
    def findLeaves(self, root: Optional[TreeNode]) -> List[List[int]]:
        d = {}
        def dfs(node: Optional[TreeNode]) -> int:
            if not node:
                return 0
            left = dfs(node.left) + 1
            right = dfs(node.right) + 1
            cur_lvl = max(left, right)
            d.setdefault(cur_lvl, []).append(node.val)
            return cur_lvl
        dfs(root)
        return [a[1] for a in sorted(d.items(), key=lambda x: x[0])]
{{< / highlight >}}
</div>
</div>
