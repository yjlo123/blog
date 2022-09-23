---
weight: 117
title: "117 Populating Next Right Pointers in Each Node II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_bfs"]
---

Given a binary tree
```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Example 1:**
```
    1            1--> NULL
   / \          / \
  2   3        2-->3--> NULL
 / \   \      / \   \
4   5   7    4-->5-->7--> NULL

Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate
each next pointer to point to its next right node, just like in Figure B.
The serialized output is in level order as connected by the next pointers,
with '#' signifying the end of each level.
```
**Example 2:**
```
Input: root = []
Output: []
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 6000]`.
- `-100 <= Node.val <= 100`
 

**Follow-up:**
- You may only use constant extra space.
- The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
"""
# Definition for a Node.
class Node:
    def __init__(
        self,
        val: int = 0,
        left: 'Node' = None,
        right: 'Node' = None,
        next: 'Node' = None
    ):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def process_child(self, child, prev, leftmost):
        if child:
            if prev:
                prev.next = child
            else:
                leftmost = child
            prev = child
        return prev, leftmost
    
    def connect(self, root: 'Node') -> 'Node':
        if not root:
            return root
        leftmost = root
        while leftmost:
            prev, cur = None, leftmost
            leftmost = None
            while cur:
                prev, leftmost = self.process_child(cur.left, prev, leftmost)
                prev, leftmost = self.process_child(cur.right, prev, leftmost)
                cur = cur.next
        return root


'''
BFS
'''
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        from collections import deque
        if not root:
            return root
        
        q = deque([root])
        while q:
            size = len(q)
            for i in range(size):
                node = q.popleft()
                if i < size - 1:
                    node.next = q[0]
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
        return root   
{{< / highlight >}}
</div>
</div>
