---
weight: 566
title: "566 Reshape the Matrix"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_matrix"]
---

In MATLAB, there is a handy function called `reshape` which can reshape an `m x n` matrix into a new one with a different size `r x c` keeping its original data.

You are given an `m x n` matrix `mat` and two integers `r` and `c` representing the number of rows and the number of columns of the wanted reshaped matrix.

The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the `reshape` operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

**Example 1:**
```
1 2  =>  1 2 3 4
3 4

Input: mat = [[1,2],[3,4]], r = 1, c = 4
Output: [[1,2,3,4]]
```
**Example 2:**
```
1 2   =>   1 2
3 4        3 4
Input: mat = [[1,2],[3,4]], r = 2, c = 4
Output: [[1,2],[3,4]]
```

**Constraints:**
- m == `mat.length`
- n == `mat[i].length`
- 1 <= m, n <= 100
- -1000 <= `mat[i][j]` <= 1000
- 1 <= r, c <= 300

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def matrixReshape(self, mat: List[List[int]], r: int, c: int) -> List[List[int]]:
        if len(mat) == 0 or not r*c == len(mat)*len(mat[0]):
            return mat
        result = []
        row = []
        for mr in mat:
            for num in mr:
                row.append(num)
                if len(row) == c:
                    result.append(row)
                    row = []
        return result
{{< / highlight >}}
</div>
</div>
