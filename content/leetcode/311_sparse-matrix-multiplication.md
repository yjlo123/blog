---
weight: 311
title: "311 Sparse Matrix Multiplication"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_hash_table"]
---

Given two [sparse matrices](sparse matrices) `mat1` of size `m x k` and `mat2` of size `k x n`, return the result of `mat1 x mat2`. You may assume that multiplication is always possible.

**Example 1:**
```
           7 0 0 
 1 0 0  x  0 0 0  =   7 0 0
-1 0 3     0 0 1     -7 0 3

Input: mat1 = [[1,0,0],[-1,0,3]], mat2 = [[7,0,0],[0,0,0],[0,0,1]]
Output: [[7,0,0],[-7,0,3]]
```
**Example 2:**
```
Input: mat1 = [[0]], mat2 = [[0]]
Output: [[0]]
```

**Constraints:**
- `m == mat1.length`
- `k == mat1[i].length == mat2.length`
- `n == mat2[i].length`
- `1 <= m, n, k <= 100`
- `-100 <= mat1[i][j], mat2[i][j] <= 100`

```
Compression:
{row: [(val, col), ...]}

[[1,0,0],   =>   {0: [( 1,0)], 
 [-1,0,3]]        1: [(-1,0), (3,2)]}

[[7,0,0],   =>   {0: [(7,0)],
 [0,0,0],         1: [(1,2)]}
 [0,0,1]] 
```


<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def multiply(
        self,
        mat1: List[List[int]],
        mat2: List[List[int]]
    ) -> List[List[int]]:
        m, k, n = len(mat1), len(mat1[0]), len(mat2[0])
        
        def compress_mat(mat: List[List[int]]) -> List[List[int]]:
            rows, cols = len(mat), len(mat[0])
            compressed = [[] for _ in range(rows)]
            for row in range(rows):
                for col in range(cols):
                    if mat[row][col]:
                        compressed[row].append((mat[row][col], col))
            return compressed
        
        A = compress_mat(mat1)
        B = compress_mat(mat2)
        
        ans = [[0] * n for _ in range(m)]
        for m1_row in range(m):
            for e1, m1_col in A[m1_row]:
                for e2, m2_col in B[m1_col]:
                    ans[m1_row][m2_col] += e1 * e2
        return ans
{{< / highlight >}}
</div>
</div>
