---
weight: 863
title: "863 All Nodes Distance K in Binary Tree"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_dfs"]
---

Given the `root` of a binary tree, the value of a `target` node target, and an integer `k`, return _an array of the values of all nodes that have a distance k from the target node_.

You can return the answer in **any order**.

**Example 1:**
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, k = 2
Output: [7,4,1]
Explanation: The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.
```
**Example 2:**
```
Input: root = [1], target = 1, k = 3
Output: []
```

**Constraints:**
- The number of nodes in the tree is in the range `[1, 500]`.
- `0 <= Node.val <= 500`
- All the values `Node.val` are **unique**.
- `target` is the value of one of the nodes in the tree.
- `0 <= k <= 1000`

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
    def distanceK(
        self,
        root: TreeNode,
        target: TreeNode,
        k: int
    ) -> List[int]:
        if k == 0:
            return [target.val]

        def dfs(node: TreeNode, parent=None) -> None:
            if not node:
                return
            node.parent = parent
            dfs(node.left, node)
            dfs(node.right, node)

        dfs(root)
        
        queue = [target]
        temp = []
        seen = {target}
        for i in range(0, k):
            if not queue:
                return []
            for n in queue:
                for nei in (n.left, n.right, n.parent):
                    if nei and nei not in seen:
                        seen.add(nei)
                        temp.append(nei)
            queue = temp
            temp = []
        return [n.val for n in queue]
{{< / highlight >}}
</div>
</div>
