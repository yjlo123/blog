---
weight: 347
title: "347 Top K Frequent Elements"
date: 2021-03-17T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_heap"]
---

Given a non-empty array of integers, return the _**k**_ most frequent elements.

**Example 1:**
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
```
**Note:**

- You may assume k is always valid, 1 ≤ _k_ ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than _O(n log n)_, where n is the array's size.
- It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
- You can return the answer in any order.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import Counter

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]: 
        if k == len(nums):
            return nums

        count = Counter(nums)   
        return heapq.nlargest(k, count.keys(), key=count.get) 
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func topKFrequent(nums []int, k int) []int {
	// count frequencies
	m := make(map[int]int)
	for _, n := range nums {
		m[n] += 1
	}

	// build a min-heap
	var heap Heap
	for num, count := range m {
		heap.pushWithMax(num, count, k)
	}

	// extract heap values
	result := make([]int, len(heap))
	for i, node := range heap {
		result[i] = node.Num
	}
	return result
}

type Node struct {
	Num   int
	Count int
}

// min-heap
type Heap []*Node

func (heap *Heap) pushWithMax(num, count, maxSize int) {
	heap.push(&Node{
		Num:   num,
		Count: count,
	})

	if len(*heap) > maxSize {
		heap.popMin()
	}
}

func (heap *Heap) push(node *Node) {
	*heap = append(*heap, node)
	i := len(*heap) - 1
	// shift up
	for i > 0 {
		parent := (i - 1) / 2
		if (*heap)[parent].Count > (*heap)[i].Count {
			heap.swap(parent, i)
			i = parent
		} else {
			break
		}
	}
}

func (heap *Heap) popMin() {
	h := *heap
	// move last to top
	(h)[0] = h[len(h)-1]
	// drop last
	*heap = h[:len(h)-1]

	// shift down
	totalLen := len(h)
	i := 0
	var smallest int
	for i < totalLen {
		li := i*2 + 1
		ri := i*2 + 2
		smallest = i
		if li < totalLen && h[li].Count < h[i].Count {
			smallest = li
		}
		if ri < totalLen && h[ri].Count < h[smallest].Count {
			smallest = ri
		}
		if smallest != i {
			heap.swap(smallest, i)
			i = smallest
			continue
		}
		break
	}
}

func (heap *Heap) swap(i, j int) {
	(*heap)[i], (*heap)[j] = (*heap)[j], (*heap)[i]
}
{{< / highlight >}}
</div>

</div>
