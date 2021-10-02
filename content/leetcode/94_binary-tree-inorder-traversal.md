---
weight: 94
title: "94 Binary Tree Inorder Traversal"
date: 2021-10-02T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

Given the `root` of a binary tree, return _the inorder traversal of its nodes' values_.

**Example 1:**
```
 1
  \
   2
  /
 3

Input: root = [1,null,2,3]
Output: [1,3,2]
```

**Example 2:**
```
Input: root = []
Output: []
```

**Example 3:**
```
Input: root = [1]
Output: [1]
```

**Example 4:**
```
   1
  /
 2

Input: root = [1,2]
Output: [2,1]
```

**Example 5:**
```
 1
  \
   2

Input: root = [1,null,2]
Output: [1,2]
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 100]`.
- -100 <= `Node.val` <= 100

**Follow up:** Recursive solution is trivial, could you do it iteratively?

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

''' Recursive '''
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        def inorder(node: Optional[TreeNode], lst: List[int]):
            if not node:
                return
            inorder(node.left, lst)
            lst.append(node.val)
            inorder(node.right, lst)
        result = []
        inorder(root, result)
        return result

''' Iterative '''
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if root is None:
            return []
        stack, res = [], []
        curr = root
        while curr or stack:
            while curr:
                stack.append(curr)
                curr = curr.left
            
            curr = stack.pop()
            res.append(curr.val) # Add after all left children
            curr = curr.right
        return res
{{< / highlight >}}
</div>
</div>
