---
weight: 86
title: "86 Partition List"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list"]
---

Given the `head` of a linked list and a value `x`, partition it such that all nodes less than `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

**Example 1:**
```
1 -> 4 -> 3 -> 2 -> 5 -> 2
            v
1 -> 2 -> 2 -> 4 -> 3 -> 5

Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```
**Example 2:**
```
Input: head = [2,1], x = 2
Output: [1,2]
```

**Constraints:**
- The number of nodes in the list is in the range `[0, 200]`.
- `-100 <= Node.val <= 100`
- `-200 <= x <= 200`

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
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        # big_dummy_head -> (greater than or equal to x)
        # small_dummy_head -> (smaller than x .. -> small_last)
        big_dummy_head = ListNode(0, head)
        small_dummy_head = small_last = ListNode()
        prev, curr = big_dummy_head, head
        while curr:
            if curr.val < x:
                prev.next = curr.next
                small_last.next = curr
                small_last =  small_last.next
            else:
                prev = curr
            curr = curr.next
        small_last.next = big_dummy_head.next
        return small_dummy_head.next
{{< / highlight >}}
</div>
</div>
