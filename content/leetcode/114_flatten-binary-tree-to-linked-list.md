---
weight: 114
title: "114 Flatten Binary Tree to Linked List"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given the `root` of a binary tree, flatten the tree into a "linked list":
- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a [pre-order traversal](https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR) of the binary tree.
 

**Example 1:**
```
    1           1
   / \           \
  2   5     =>    2
 / \   \           \
3   4   6           3
                     \
                      4
                       \
                        5
                         \
                          6

Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
```
**Example 2:**
```
Input: root = []
Output: []
```
**Example 3:**
```
Input: root = [0]
Output: [0]
```

Constraints:

The number of nodes in the tree is in the range [0, 2000].
-100 <= Node.val <= 100
 

Follow up: Can you flatten the tree in-place (with O(1) extra space)?

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

    def __init__(self):
        self.stack = []

    def flatten(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if not root:
            return
        
        if root.right:
            self.stack.append(root.right)

        if root.left:
            root.right = root.left
        elif self.stack:
            root.right = self.stack.pop()
        
        self.flatten(root.right)
        root.left = None


'''
O(1) space
'''
class Solution:
    
    def flatten(self, root: TreeNode) -> None:
        if not root:
            return None
        
        node = root
        while node:
            if node.left:
                rightmost = node.left
                while rightmost.right:
                    rightmost = rightmost.right

                rightmost.right = node.right
                node.right = node.left
                node.left = None
            
            # move on to the right side of the tree
            node = node.right
{{< / highlight >}}
</div>
</div>
