---
weight: 304
title: "304 Range Sum Query 2D - Immutable"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix"]
---

Given a 2D matrix `matrix`, handle multiple queries of the following type:
- Calculate the **sum** of the elements of matrix inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.

Implement the `NumMatrix` class:
- `NumMatrix(int[][] matrix)` Initializes the object with the integer matrix `matrix`.
- `int sumRegion(int row1, int col1, int row2, int col2)` Returns the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.
You must design an algorithm where `sumRegion` works on `O(1)` time complexity.

**Example 1:**
```

Input
["NumMatrix", "sumRegion", "sumRegion", "sumRegion"]
[
    [
        [
            [3, 0, 1, 4, 2],
            [5, 6, 3, 2, 1],
            [1, 2, 0, 1, 5],
            [4, 1, 0, 1, 7],
            [1, 0, 3, 0, 5]
        ]
    ],
    [2, 1, 4, 3],
    [1, 1, 2, 2],
    [1, 2, 2, 4]
]
Output
[null, 8, 11, 12]

Explanation
NumMatrix numMatrix = new NumMatrix(
    [
        [3, 0, 1, 4, 2],
        [5, 6, 3, 2, 1],
        [1, 2, 0, 1, 5],
        [4, 1, 0, 1, 7],
        [1, 0, 3, 0, 5]
    ]);
numMatrix.sumRegion(2, 1, 4, 3); // return 8 (i.e sum of the red rectangle)
numMatrix.sumRegion(1, 1, 2, 2); // return 11 (i.e sum of the green rectangle)
numMatrix.sumRegion(1, 2, 2, 4); // return 12 (i.e sum of the blue rectangle)
```

**Constraints:**
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- <code>-10<sup>4</sup> <= matrix[i][j] <= 10<sup>4</sup></code>
- `0 <= row1 <= row2 < m`
- `0 <= col1 <= col2 < n`
- At most <code>10<sup>4</sup></code> calls will be made to `sumRegion`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        self.matrix = matrix
        m = len(matrix)
        n = len(matrix[0])
        self.dp = [[0]*(n+1) for _ in range(m+1)]
        for i in range(1, m+1):
            for j in range(1, n+1):
                self.dp[i][j] = (
                    matrix[i-1][j-1]
                    + self.dp[i-1][j]
                    + self.dp[i][j-1]
                    - self.dp[i-1][j-1]
                )

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        return (
            self.dp[row2+1][col2+1]
            - self.dp[row2+1][col1]
            - self.dp[row1][col2+1]
            + self.dp[row1][col1]
        )

# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
{{< / highlight >}}
</div>
</div>
