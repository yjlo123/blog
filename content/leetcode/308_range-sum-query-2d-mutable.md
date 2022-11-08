---
weight: 308
title: "308 Range Sum Query 2D - Mutable"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_matrix"]
---

Given a 2D matrix `matrix`, handle multiple queries of the following types:

**Update** the value of a cell in `matrix`.
Calculate the sum of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.
Implement the NumMatrix class:
- `NumMatrix(int[][] matrix)` Initializes the object with the integer matrix `matrix`.
- `void update(int row, int col, int val)` **Updates** the value of `matrix[row][col]` to be `val`.
- `int sumRegion(int row1, int col1, int row2, int col2)` Returns the sum of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.

**Example 1:**
```
Input
["NumMatrix", "sumRegion", "update", "sumRegion"]
[[[[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]], [2, 1, 4, 3], [3, 2, 2], [2, 1, 4, 3]]
Output
[null, 8, null, 10]

Explanation
NumMatrix numMatrix = new NumMatrix([[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]);
numMatrix.sumRegion(2, 1, 4, 3); // return 8 (i.e. sum of the left red rectangle)
numMatrix.update(3, 2, 2);       // matrix changes from left image to right image
numMatrix.sumRegion(2, 1, 4, 3); // return 10 (i.e. sum of the right red rectangle)
```

**Constraints:**
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- <code>-10<sup>5</sup> <= matrix[i][j] <= 10<sup>5</sup></code>
- `0 <= row < m`
- `0 <= col < n`
- <code>-10<sup>5</sup> <= val <= 10<sup>5</sup></code>
- `0 <= row1 <= row2 < m`
- `0 <= col1 <= col2 < n`
- At most <code>10<sup>4</sup></code> calls will be made to `sumRegion` and `update`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        for row in matrix:
            for col in range(1, len(row)):
                row[col] += row[col-1]
        self.matrix = matrix

    def update(self, row: int, col: int, val: int) -> None:
        original = self.matrix[row][col]
        if col != 0:
            original -= self.matrix[row][col-1]
            
        diff = original - val
        
        for y in range(col, len(self.matrix[0])):
            self.matrix[row][y] -= diff

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        res = 0
        for x in range(row1, row2+1):
            res += self.matrix[x][col2]
            if col1 != 0:
                res -= self.matrix[x][col1-1]
        return res


# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# obj.update(row,col,val)
# param_2 = obj.sumRegion(row1,col1,row2,col2)
{{< / highlight >}}
</div>
</div>
