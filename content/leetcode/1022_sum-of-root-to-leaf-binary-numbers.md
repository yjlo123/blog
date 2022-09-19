---
weight: 1022
title: "1022 Sum of Root To Leaf Binary Numbers"
date: 2021-03-24T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

You are given the `root` of a binary tree where each node has a value `0` or `1`.  Each root-to-leaf path represents a binary number starting with the most significant bit.  
- For example, if the path is `0 -> 1 -> 1 -> 0 -> 1`, then this could represent `01101` in binary, which is `13`.

For all leaves in the tree, consider the numbers represented by the path from the root to that leaf. Return _the sum of these numbers_.

The test cases are generated so that the answer fits in a **32-bits** integer.

**Example 1:**
```
      1
    /   \
  0       1
 / \     / \
0   1   0   1

Input: root = [1,0,1,0,1,0,1]
Output: 22
Explanation: (100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22
```
**Example 2:**
```
Input: root = [0]
Output: 0
```
**Example 3:**
```
Input: root = [1]
Output: 1
```
**Example 4:**
```
Input: root = [1,1]
Output: 3
```

**Constraints:**
- The number of nodes in the tree is in the range `[1, 1000]`.
- `Node.val` is `0` or `1`.

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
    def sumRootToLeaf(self, root: Optional[TreeNode]) -> int:
        return self.dfs(root, 0)
    
    def dfs(self, node: Optional[TreeNode], current: int) -> int:
        if not node:
            return 0
        current = (current << 1) + node.val
        if node.left == node.right:
            return current
        return self.dfs(node.left, current) + self.dfs(node.right, current)
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumRootToLeaf(root *TreeNode) int {
    return sum(root, 0)
}

func sum(tree *TreeNode, num int) int {
    if tree == nil {
        return 0
    }
    currentVal := num << 1 + tree.Val
    if tree.Left == nil && tree.Right == nil {
        return currentVal
    }
    return sum(tree.Left, currentVal) + sum(tree.Right, currentVal)
}
{{< / highlight >}}
</div>
</div>
