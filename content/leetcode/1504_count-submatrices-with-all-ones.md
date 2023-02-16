---
weight: 1504
title: "1504 Count Submatrices With All Ones"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_dp"]
---

Given an `m x n` binary matrix `mat`, return *the number of **submatrices** that have all ones*.

**Example 1:**
```
1 0 1
1 1 0
1 1 0

Input: mat = [[1,0,1],[1,1,0],[1,1,0]]
Output: 13
Explanation: 
There are 6 rectangles of side 1x1.
There are 2 rectangles of side 1x2.
There are 3 rectangles of side 2x1.
There is 1 rectangle of side 2x2. 
There is 1 rectangle of side 3x1.
Total number of rectangles = 6 + 2 + 3 + 1 + 1 = 13.
```
**Example 2:**
```
0 1 1 0
0 1 1 1
1 1 1 0

Input: mat = [[0,1,1,0],[0,1,1,1],[1,1,1,0]]
Output: 24
Explanation: 
There are 8 rectangles of side 1x1.
There are 5 rectangles of side 1x2.
There are 2 rectangles of side 1x3. 
There are 4 rectangles of side 2x1.
There are 2 rectangles of side 2x2. 
There are 2 rectangles of side 3x1. 
There is 1 rectangle of side 3x2. 
Total number of rectangles = 8 + 5 + 2 + 4 + 2 + 2 + 1 = 24.
```

**Constraints:**
- `1 <= m, n <= 150`
- `mat[i][j]` is either `0` or `1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numSubmat(self, mat: List[List[int]]) -> int:
        m, n = len(mat), len(mat[0])
        for i in range(m):
            for j in range(1, n):
                if mat[i][j]:
                    mat[i][j] = mat[i][j-1] + 1
        
        res = 0
        '''
        For each 1 within a row, count the submatrices that contain
        the 1 and start on the same row either at the 1 or to the
        left of the 1. Proceed down the column that contains the 1
        until reaching a 0 or the bottom row of the matrix. While
        proceeding down a column, the width of the submatrices stays
        the same or gets thinner.
        '''
        for i in range(m):
            for j in range(n):
                if mat[i][j] == 0:
                    continue
                row = i
                width = mat[i][j]
                while row < m and mat[row][j]:
                    width = min(width, mat[row][j])
                    res += width
                    row += 1
        return res


'''
Faster DP
'''
class Solution:
    def numSubmat(self, mat: List[List[int]]) -> int:
        m, n =len(mat), len(mat[0])
        res = 0
        histogram = [0] * (n+1)
        for i in range(m):
            stack, dp = [-1], [0] * (n+1)
            for j in range(n):
                histogram[j] = 0 if mat[i][j] == 0 else histogram[j] + 1
                while histogram[j] < histogram[stack[-1]]:
                    stack.pop()
                vertical_choices = histogram[j]
                horizontal_choices = j - stack[-1]
                dp[j] = dp[stack[-1]] + vertical_choices * horizontal_choices
                res += dp[j]
                stack.append(j)
        return res
{{< / highlight >}}
</div>
</div>
