---
weight: 74
title: "74 Search a 2D Matrix"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_binary_search"]
---

Write an efficient algorithm that searches for a value in an `m x n` matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

**Example 1:**
```
 1  (3)  5   7
10  11  16  20
23  30  34  60

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```
**Example 2:**
```
 1   3   5   7
10  11  16  20
23  30  34  60

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```

**Constraints:**
- m == `matrix.length`
- n == `matrix[i].length`
- 1 <= m, n <= 100
- -10<sup>4</sup> <= `matrix[i][j]`, target <= 10<sup>4</sup>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        def binary_search(lst, l, m):
            if l == m:
                return l, lst[l] == target
            mid = (l + m + 1) // 2
            if lst[mid] == target:
                return mid, True
            if lst[mid] > target:
                return binary_search(lst, l, mid-1)
            return binary_search(lst, mid, m)
        
        heads = [r[0] for r in matrix]
        row, _ = binary_search(heads, 0, len(heads)-1)
        _, res = binary_search(matrix[row], 0, len(matrix[0])-1)
        return res
{{< / highlight >}}
</div>
</div>
