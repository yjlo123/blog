---
weight: 103
title: "103 Binary Tree Zigzag Level Order Traversal"
date: 2021-03-21T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_bfs"]
---

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**
```
     3
    / \
   9   20
      /  \
     15   7

Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```
**Example 2:**
```
Input: root = [1]
Output: [[1]]
```
**Example 3:**
```
Input: root = []
Output: []
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 2000]`.
- `-100 <= Node.val <= 100`

> BFS level by level

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
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        res = []
        direction = 1
        level = [root]
        while level:
            res.append([n.val for n in level][::direction])
            direction *= -1
            level = [
                child
                for node in level
                for child in (node.left, node.right)
                if child
            ]
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

func traverseTree(root *TreeNode, level int, result *[][]int) {
    if root == nil {
        return
    }
    if level > len(*result)-1 {
        *result = append(*result, []int{})
    }
    (*result)[level] = append((*result)[level], root.Val)

    traverseTree(root.Left, level+1, result)
    traverseTree(root.Right, level+1, result)

}

func reverse(nums []int) {
    for i := 0; i < len(nums)/2; i++ {
        j := len(nums) - i - 1
        nums[i], nums[j] = nums[j], nums[i]
    }
}

func zigzagLevelOrder(root *TreeNode) [][]int {
    var result [][]int
    traverseTree(root, 0, &result)
    for i := 1; i < len(result); i += 2 {
        reverse(result[i])
    }
    return result
}
{{< / highlight >}}
</div>

</div>
