---
weight: 83
title: "83 Remove Duplicates from Sorted List"
date: 2021-10-02T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_linked_list"]
---
Given the `head` of a sorted linked list, _delete all duplicates such that each element appears only once. Return the linked list **sorted** as well_.

**Example 1:**
```
1 -> 1 -> 2
     |
     v
   1 -> 2

Input: head = [1,1,2]
Output: [1,2]
```
**Example 2:**
```
1 -> 1 -> 2 -> 3 -> 3
         |
         v
    1 -> 2 -> 3

Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

**Constraints:**

- The number of nodes in the list is in the range `[0, 300]`.
- -100 <= `Node.val` <= 100
- The list is guaranteed to be **sorted** in ascending order.


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
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        head.next = self.deleteDuplicates(head.next)
        if head.val == head.next.val:
            return head.next
        return head

''' Iterative '''
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while current and current.next:
            if current.next.val == current.val:
                current.next = current.next.next
            else:
                current = current.next
        return head
{{< / highlight >}}
</div>
</div>
