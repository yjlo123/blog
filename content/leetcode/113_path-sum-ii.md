---
weight: 113
title: "113 Path Sum II"
date: 2021-03-25T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the `root` of a binary tree and an integer `targetSum`, return all **root-to-leaf** paths where each path's sum equals `targetSum`.

A **leaf** is a node with no children.

**Example 1:**
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1

Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
```
**Example 2:**
```
    1
   / \
  2   3

Input: root = [1,2,3], targetSum = 5
Output: []
```
**Example 3:**
```
Input: root = [1,2], targetSum = 0
Output: []
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- -1000 <= `Node.val` <= 1000
- -1000 <= `targetSum` <= 1000

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
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        res = []
        def dfs(node, path, total):
            if not node:
                return
            new_val = node.val + total
            new_path = path + [node.val]
            if node.left == node.right and new_val == targetSum:
                res.append(new_path)
                return
            dfs(node.left, new_path, new_val)
            dfs(node.right, new_path, new_val)
        dfs(root, [], 0)
        return res
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

func pathSum(root *TreeNode, targetSum int) [][]int {
	var result [][]int
	sum(root, targetSum, 0, nil, &result)
	return result
}

func sum(t *TreeNode, target, curSum int, curPath []int, result *[][]int) {
	if t == nil {
		return
	}
	curPath = append(curPath, t.Val)
	if t.Left == nil && t.Right == nil {
		if curSum+t.Val == target {
            // Important!
            // func arg curPath is a slice reference
            // its underlying data could be changed in another resursion
            // so we make a copy
			res := make([]int, len(curPath))
			copy(res, curPath)
			*result = append(*result, res)
		}
		return
	}
	if t.Left != nil {
		sum(t.Left, target, curSum+t.Val, curPath, result)
	}
	if t.Right != nil {
		sum(t.Right, target, curSum+t.Val, curPath, result)
	}
}
{{< / highlight >}}
</div>
</div>
