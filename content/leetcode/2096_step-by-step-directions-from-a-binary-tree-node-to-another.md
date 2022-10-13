---
weight: 2096
title: "2096 Step-By-Step Directions From a Binary Tree Node to Another"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs", "lc_tree"]
---

You are given the `root` of a **binary tree** with `n` nodes. Each node is uniquely assigned a value from `1` to `n`. You are also given an integer `startValue` representing the value of the start node `s`, and a different integer `destValue` representing the value of the destination node `t`.

Find the **shortest path** starting from node `s` and ending at node `t`. Generate step-by-step directions of such path as a string consisting of only the uppercase letters `'L'`, `'R'`, and `'U'`. Each letter indicates a specific direction:
- `'L'` means to go from a node to its **left child** node.
- `'R'` means to go from a node to its **right child** node.
- `'U'` means to go from a node to its **parent** node.

Return _the step-by-step directions of the **shortest path** from node `s` to node `t`_.

**Example 1:**
```
    5
   / \
  1   2
 /   / \
3   6   4

Input: root = [5,1,2,3,null,6,4], startValue = 3, destValue = 6
Output: "UURL"
Explanation: The shortest path is: 3 → 1 → 5 → 2 → 6.
```
**Example 2:**
```
  2
 /
1

Input: root = [2,1], startValue = 2, destValue = 1
Output: "L"
Explanation: The shortest path is: 2 → 1.
```

**Constraints:**
- The number of nodes in the tree is `n`.
- <code>2 <= n <= 10<sup>5</sup></code>
- `1 <= Node.val <= n`
- All the values in the tree are unique.
- `1 <= startValue, destValue <= n`
- `startValue != destValue`

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
    def getDirections(
        self,
        root: Optional[TreeNode],
        startValue: int,
        destValue: int
    ) -> str:
        def find_path(node: Optional[TreeNode]) -> bool:
            if not node:
                return False
            elif node.val == startValue:
                paths[0] = ''.join(path)
            elif node.val == destValue:
                paths[1] = ''.join(path)

            if paths[0] and paths[1]:
                return True

            path.append('L')
            if find_path(node.left):
                return True
            path.pop()
            
            path.append('R')
            if find_path(node.right):
                return True
            path.pop()
            return False

        paths = ['', '']
        path = []
        find_path(root)
        p1, p2 = paths

        common_len = 0
        for i in range(min(len(p1), len(p2))):
            if p1[i] == p2[i]:
                common_len += 1
            else:
                break
        return 'U' * (len(p1) - common_len) + p2[common_len:]
{{< / highlight >}}
</div>
</div>
