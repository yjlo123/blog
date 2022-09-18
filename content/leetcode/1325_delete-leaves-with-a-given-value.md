---
weight: 1325
title: "1325 Delete Leaves With a Given Value"
date: 2021-03-28T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given a binary tree `root` and an integer `target`, delete all the **leaf nodes** with value `target`.

Note that once you delete a leaf node with value `target`, if it's parent node becomes a leaf node and has the value `target`, it should also be deleted (you need to continue doing that until you cannot).

**Example 1:**
```
     1               1           1
    / \             / \           \
   2   3     =>   (2)  3     =>    3
  /   / \               \           \
(2) (2)  4               4           4

Input: root = [1,2,3,2,null,2,4], target = 2
Output: [1,null,3,null,4]
Explanation: Leaf nodes in green with value (target = 2) are removed (Picture in left). 
After removing, new nodes become leaf nodes with value (target = 2) (Picture in center).
```
**Example 2:**
```
     1             1
    / \           /
   3  (3)   =>   3
  / \             \
(3)  2             2

Input: root = [1,3,3,3,2], target = 3
Output: [1,3,null,null,2]
```
**Example 3:**
```
       1            1           1          1
      /            /           /
     2            2          (2)
    /      =>    /      =>           =>
   2           (2)
  /
(2)

Input: root = [1,2,null,2,null,2], target = 2
Output: [1]
Explanation: Leaf nodes in green with value (target = 2) are removed at each step.
```
**Example 4:**
```
Input: root = [1,1,1], target = 1
Output: []
```
**Example 5:**
```
Input: root = [1,2,3], target = 1
Output: [1,2,3]
```

**Constraints:**
- The number of nodes in the tree is in the range `[1, 3000]`.
- `1 <= Node.val, target <= 1000`

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
    def removeLeafNodes(
        self,
        root: Optional[TreeNode],
        target: int
    ) -> Optional[TreeNode]:
        if root.left:
            root.left = self.removeLeafNodes(root.left, target)
        if root.right:
            root.right = self.removeLeafNodes(root.right, target)
        if root.left == root.right and root.val == target:
            return None
        return root
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func removeLeafNodes(root *TreeNode, target int) *TreeNode {
    if root.Left != nil {
        root.Left = removeLeafNodes(root.Left, target)
    }

    if root.Right != nil {
        root.Right = removeLeafNodes(root.Right, target)
    }

    if root.Left == root.Right && root.Val == target {
        return nil
    }

    return root
}
{{< / highlight >}}
</div>
</div>
