---
weight: 48
title: "48 Rotate Image"
date: 2021-03-19T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix"]
---

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [in-place](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**
```
1 2 3      7 4 1
4 5 6  =>  8 5 2
7 8 9      9 6 3

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```
**Example 2:**
```
5  1  9  11      15 13 2  5
2  4  8  10  =>  14 3  4  1
13 3  6  7       12 6  8  9
15 14 12 16      16 7  10 11

Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```
**Example 3:**
```
Input: matrix = [[1]]
Output: [[1]]
```
**Example 4:**
```
Input: matrix = [[1,2],[3,4]]
Output: [[3,1],[4,2]]
```

**Constraints:**
- `n == matrix.length == matrix[i].length`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func rotate(matrix [][]int) {
	n := len(matrix) - 1
	// reverse up to down
	for i := 0; i < len(matrix)/2; i++ {
		for j := 0; j < len(matrix); j++ {
			// swap (i, j), (n-i, j)
			matrix[i][j], matrix[n-i][j] = matrix[n-i][j], matrix[i][j]
		}
	}
	// swap the symmetry
	for i := 0; i < len(matrix); i++ {
		for j := i + 1; j < len(matrix); j++ {
			// swap (i, j), (j, i)
			matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
		}
	}
}
{{< / highlight >}}
</div>
</div>
