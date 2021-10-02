---
weight: 203
title: "203 Remove Linked List Elements"
date: 2021-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_linked_list"]
---
Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return _the new head_.

**Example 1:**
```
1 -> 2 -> (6) -> 3 -> 4 -> 5 -> (6)
               |
               v
      1 -> 2 -> 3-> 4 -> 5

Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
```
**Example 2:**
```
Input: head = [], val = 1
Output: []
```
**Example 3:**
```
Input: head = [7,7,7,7], val = 7
Output: []
 ```

**Constraints:**

- The number of nodes in the list is in the range [0, 10<sup>4</sup>].
- 1 <= `Node.val` <= 50
- 0 <= val <= 50

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

''' Recursive '''
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        if not head:
            return head
        head.next = self.removeElements(head.next, val)
        return head.next if head.val == val else head

''' Iterative '''
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        sentinel = ListNode(0)
        sentinel.next = head
        
        prev, curr = sentinel, head
        while curr:
            if curr.val == val:
                prev.next = curr.next
            else:
                prev = curr
            curr = curr.next
        
        return sentinel.next
{{< / highlight >}}
</div>
</div>
