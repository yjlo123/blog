---
weight: 141
title: "141 Linked List Cycle"
date: 2021-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_linked_list", "hash_table", "two_pointers"]
---

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's next pointer is connected to. **Note that `pos` is not passed as a parameter.**

Return `true` _if there is a cycle in the linked list_. Otherwise, return `false`.

**Example 1:**
```
[3] -> [2] -> [0] -> [4]
        ^_____________|

Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

**Example 2:**
```
[1] -> [2]
 ^______|

Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```

**Example 3:**
```
[1]

Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

**Constraints:**
- The number of the nodes in the list is in the range [0, 10<sup>4</sup>].
- -10<sup>5</sup> <= `Node.val` <= 10<sup>5</sup>
- `pos` is `-1` or a valid index in the linked-list.

**Follow up:**
Can you solve it using O(1) (i.e. constant) memory?

<div class="tabs"></div>
<div class="tab-content">

<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

''' Set '''
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        seen = set()
        while head != None:
            if head not in seen:
                seen.add(head)
                head = head.next
            else:
                return True
        return False

''' Two pointers '''
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        p1 = p2 = head
        while p2 is not None and p2.next is not None:
            p1 = p1.next
            p2 = p2.next.next
            if p1 == p2:
                return True
        return False
{{< / highlight >}}
</div>
</div>
