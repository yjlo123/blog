---
weight: 938
title: "938 Range Sum of BST"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_dfs"]
---

Given the `root` node of a binary search tree and two integers `low` and `high`, return *the sum of values of all nodes with a value in the **inclusive** range `[low, high]`*.


**Example 1:**
```
    10
   /  \
  5    15
 / \    \
3   7    18

Input: root = [10,5,15,3,7,null,18], low = 7, high = 15
Output: 32
Explanation: Nodes 7, 10, and 15 are in the range [7, 15]. 7 + 10 + 15 = 32.
```
**Example 2:**
```
       10
     /    \
    5      15
   / \    /  \
  3   7  13   18
 /   /
1   6

Input: root = [10,5,15,3,7,13,18,1,null,6], low = 6, high = 10
Output: 23
Explanation: Nodes 6, 7, and 10 are in the range [6, 10]. 6 + 7 + 10 = 23.
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[1, 2 * 10<sup>4</sup>]</code>.
- <code>1 <= Node.val <= 10<sup>5</sup></code>
- <code>1 <= low <= high <= 10<sup>5</sup></code>
- All `Node.val` are unique.

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
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        def dfs(node: Optional[TreeNode]):
            if not node:
                return
            if low <= node.val <= high:
                self.sum += node.val
            if node.val > low:
                dfs(node.left)
            if node.val < high:
                dfs(node.right)

        self.sum = 0
        dfs(root)
        return self.sum
{{< / highlight >}}
</div>
</div>
