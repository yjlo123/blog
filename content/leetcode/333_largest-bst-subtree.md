---
weight: 333
title: "333 Largest BST Subtree"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the root of a binary tree, find the largest subtree, which is also a Binary Search Tree (BST), where the largest means subtree has the largest number of nodes.

A **Binary Search Tree (BST)** is a tree in which all the nodes follow the below-mentioned properties:
- The left subtree values are less than the value of their parent (root) node's value.
- The right subtree values are greater than the value of their parent (root) node's value.

**Note**: A subtree must include all of its descendants.

**Example 1:**
```
     10
    /  \
  (5)   15
  / \    \
(1) (8)   7

Input: root = [10,5,15,1,8,null,7]
Output: 3
Explanation: The Largest BST Subtree in this case is the highlighted one.
The return value is the subtree's size, which is 3.
```
**Example 2:**
```
Input: root = [4,2,7,2,3,5,null,2,null,null,null,null,null,1]
Output: 2
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.
- <code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code>
 

**Follow up:** Can you figure out ways to solve it with `O(n)` time complexity?

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
    def largestBSTSubtree(self, root: Optional[TreeNode]) -> int:
        def dfs(node) -> (int, int, int):
            if not node:
                return 0, float('inf'), float('-inf')
            
            left_max_size, left_min, left_max = dfs(node.left)
            right_max_size, right_min, right_max = dfs(node.right)
            
            if left_max < node.val < right_min:
                # is a BST
                return (
                    left_max_size + right_max_size + 1,
                    min(node.val, left_min),
                    max(node.val, right_max),
                )
            
            return (
                max(left_max_size, right_max_size),
                float('-inf'),
                float('inf'),
            )
        
        return dfs(root)[0]
{{< / highlight >}}
</div>
</div>
