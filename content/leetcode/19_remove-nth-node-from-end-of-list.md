---
weight: 19
title: "19 Remove Nth Node From End of List"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list", "lc_two_pointers"]
---

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**
```
1 -> 2 -> 3 -> (4) -> 5

1 -> 2 -> 3 --------> 5

Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**
```
Input: head = [1], n = 1
Output: []
```

**Example 3:**
```
Input: head = [1,2], n = 1
Output: [1]
```

**Constraints:**
- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

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
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        fast = slow = dummy
        for i in range(n+1):
            fast = fast.next

        while fast:
            fast = fast.next
            slow = slow.next

        slow.next = slow.next.next
        return dummy.next
{{< / highlight >}}
</div>
</div>
