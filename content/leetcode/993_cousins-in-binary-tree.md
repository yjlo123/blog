---
weight: 993
title: "993 Cousins in Binary Tree"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree", "lc_bfs"]
---

Given the `root` of a binary tree with unique values and the values of two different nodes of the tree `x` and `y`, return _`true` if the nodes corresponding to the values `x` and `y` in the tree are **cousins**, or `false` otherwise_.

Two nodes of a binary tree are **cousins** if they have the same depth with different parents.

Note that in a binary tree, the root node is at the depth `0`, and children of each depth k node are at the depth `k + 1`.

**Example 1:**
```
    1
   / \
  2   3
 /
4

Input: root = [1,2,3,4], x = 4, y = 3
Output: false
```
**Example 2:**
```
    1
   / \
  2   3
  \    \
   4    5

Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
```
**Example 3:**
```
    1
   / \
  2   3
  \
   4

Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
```

**Constraints:**
- The number of nodes in the tree is in the range `[2, 100]`.
- `1 <= Node.val <= 100`
- Each node has a **unique** value.
- `x != y`
- `x` and `y` are exist in the tree.

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
    def isCousins(self, root: Optional[TreeNode], x: int, y: int) -> bool:
        level = [root]
        target_lvl = -1
        current_lvl = 0
        while level:
            temp_level = []
            values = set()
            for node in level:
                current_children = set()
                if node.left:
                    temp_level.append(node.left)
                    current_children.add(node.left.val)
                if node.right:
                    temp_level.append(node.right)
                    current_children.add(node.right.val) 
                if x in current_children and y in current_children:
                        return False
                values |= current_children
            if x in values and y in values:
                return True
            if (
                (x in values and y not in values)
                or (x not in values and y in values)
            ):
                return False
            level = temp_level
        return False


'''
DFS
'''
class Solution:
    def isCousins(self, root: TreeNode, x: int, y: int) -> bool:
        def dfs(node, parent, depth, v):
            if node:
                if node.val == v:
                    return depth, parent
                return (
                    dfs(node.left, node, depth + 1, v)
                    or dfs(node.right, node, depth + 1, v)
                )
        dx, px = dfs(root, None, 0, x)
        dy, py = dfs(root, None, 0, y)
        return dx == dy and px != py
{{< / highlight >}}
</div>
</div>
