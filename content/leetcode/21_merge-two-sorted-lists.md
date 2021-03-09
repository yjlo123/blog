---
weight: 21
title: "21 Merge Two Sorted Lists"
date: 2020-10-18T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_linked_list"]
---

Merge two sorted linked lists and return it as a new **sorted** list. The new list should be made by splicing together the nodes of the first two lists.

**Example 1:**
```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

**Example 2:**
```
Input: l1 = [], l2 = []
Output: []
```

**Example 3:**
```
Input: l1 = [], l2 = [0]
Output: [0]
```

**Constraints:**

- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `l1` and `l2` are sorted in **non-decreasing** order.

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
	if l1 == nil {
		return l2
	}
	if l2 == nil {
		return l1
	}

	result := ListNode{}
	if l1.Val < l2.Val {
		result.Val = l1.Val
		result.Next = mergeTwoLists(l1.Next, l2)
	} else {
		result.Val = l2.Val
		result.Next = mergeTwoLists(l1, l2.Next)
	}
	return &result
}
{{< / highlight >}}
</div>
<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if(l1 == null){
        return l2;
    }
    if(l2 == null){
        return l1;
    }
    
    ListNode mergeHead;
    if(l1.val < l2.val){
        mergeHead = l1;
        mergeHead.next = mergeTwoLists(l1.next, l2);
    }
    else{
        mergeHead = l2;
        mergeHead.next = mergeTwoLists(l1, l2.next);
    }
    return mergeHead;
}
{{< / highlight >}}
</div>
<div id="runtime" class="lang">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode21" target="_blank">https://runtime.siwei.dev/?src=leetcode21</a>
    </div>
</div>
</div>
