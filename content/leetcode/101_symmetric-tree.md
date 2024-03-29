---
weight: 101
title: "101 Symmetric Tree"
date: 2021-03-20T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

 

**Example 1:**
```
      1
    /   \
  2       2
 / \     / \
3   4   4   3

Input: root = [1,2,2,3,4,4,3]
Output: true
```
**Example 2:**
```
      1
    /   \
  2       2
   \       \
    3       3

Input: root = [1,2,2,null,3,null,3]
Output: false
```

**Constraints:**
- The number of nodes in the tree is in the range [1, 1000].
- -100 <= Node.val <= 100
 

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
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        def checkSymmetry(
            left: Optional[TreeNode],
            right: Optional[TreeNode]
        ) -> bool:
            if not left or not right:
                return left == right
            if left.val != right.val:
                return False
            return (
                checkSymmetry(left.left, right.right)
                and checkSymmetry(left.right, right.left)
            )

        return checkSymmetry(root.left, root.right)
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
func isSymmetric(root *TreeNode) bool {
	return root != nil && checkSymmetry(root.Left, root.Right)
}

func checkSymmetry(left *TreeNode, right *TreeNode) bool {
	if left == nil || right == nil {
		return left == right
	}
	if left.Val != right.Val {
		return false
	}
	return checkSymmetry(left.Left, right.Right) && checkSymmetry(left.Right, right.Left)
}
{{< / highlight >}}
</div>

<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public boolean isSymmetric(TreeNode root) {
        return (root == null) || help(root.left, root.right);
    }
    
    private boolean help(TreeNode l, TreeNode r){
        if (l == null || r == null) return l == r;
        if(l.val != r.val) return false;
        return help(l.left, r. right) && help(l.right, r.left);
    }
}
{{< / highlight >}}
</div>
</div>
