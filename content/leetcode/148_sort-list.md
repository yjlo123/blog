---
weight: 148
title: "148 Sort List"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list", "lc_sorting"]
---

Given the `head` of a linked list, return *the list after sorting it in **ascending order***.


**Example 1:**
```
4 -> 2 -> 1 -> 3
       v
1 -> 2 -> 3 -> 4

Input: head = [4,2,1,3]
Output: [1,2,3,4]
```
**Example 2:**
```
-1 -> 5 -> 3 -> 4 -> 0
           v
-1 -> 0 -> 3 -> 4 -> 5

Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```
**Example 3:**
```
Input: head = []
Output: []
```

**Constraints:**
- The number of nodes in the list is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.
- <code>-10<sup>5</sup> <= Node.val <= 10<sup>5</sup></code>
 

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or head.next is None:
            return head
        left = head
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        right = slow.next
        slow.next = None
        l1 = self.sortList(left)
        l2 = self.sortList(right)
        return self.mergeList(l1, l2)
    
    def mergeList(
        self,
        l1: Optional[ListNode],
        l2: Optional[ListNode]
    ) -> Optional[ListNode]:
        if not l1 or not l2:
            return l1 or l2
        dummy = prev = ListNode()
        while l1 and l2:
            if l1.val > l2.val:
                prev.next = l2
                l2 = l2.next
            else:
                prev.next = l1
                l1 = l1.next
            prev = prev.next
        prev.next = l1 or l2
        return dummy.next
{{< / highlight >}}
</div>
</div>
