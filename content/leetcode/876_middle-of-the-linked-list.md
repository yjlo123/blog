---
weight: 876
title: "876 Middle of the Linked List"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_linked_list", "lc_two_pointers"]
---

Given the `head` of a singly linked list, return the _middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

**Example 1:**
```
1 -> 2 -> (3) -> 4 -> 5

Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```

**Example 2:**
```
1 -> 2 -> 3 -> (4) -> 5 -> 6

Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```

**Constraints:**
- The number of nodes in the list is in the range `[1, 100]`.
- 1 <= Node.val <= 100

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
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        return slow
{{< / highlight >}}
</div>
</div>
