---
weight: 200
title: "200 Number of Islands"
date: 2020-12-10T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_matrix", "lc_dfs", "lc_union_find"]
---

Given an `m x n` 2d `grid` map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.


**Example 1:**
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```
**Example 2:**
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
 ```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

> **DFS/BFS**:  DFS/BFS over all unvisited nodes and count the number of initial DFS/BFS calls.  
> **Union Find**:  For each land node, union it with its neighbor land.


<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        
        def dfs(row: int, col: int) -> None:
            grid[row][col] = '2'
            for dr, dc in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                r, c = row + dr, col + dc
                if 0 <= r < m and 0 <= c < n and grid[r][c] == '1':
                    dfs(r, c)
        count = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    count += 1
                    dfs(i, j)
        return count



'''
Union Find
'''
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0

        m, n = len(grid), len(grid[0])
        self.count = sum(grid[i][j] == '1' for i in range(m) for j in range(n))
        parent = [i for i in range(m * n)]
        
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]

        def union(x, y):
            xroot, yroot = find(x), find(y)
            if xroot == yroot:
                return
            parent[xroot] = yroot
            self.count -= 1

        for i in range(m):
            for j in range(n):
                if grid[i][j] == '0':
                    continue
                idx = i * n + j
                if j < n-1 and grid[i][j+1] == '1':
                    union(idx, idx+1)
                if i < m-1 and grid[i+1][j] == '1':
                    union(idx, idx+n)
        return self.count
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func numIslands(grid [][]byte) int {
	if grid == nil || len(grid) == 0 {
		return 0
	}

	count := 0
	for i := 0; i < len(grid); i++ {
		for j := 0; j < len(grid[i]); j++ {
			if grid[i][j] == '1' {
				count += dfs(grid, i, j)
			}
		}
	}
	return count
}

func dfs(grid [][]byte, i, j int) int {
	if i < 0 || i >= len(grid) || j < 0 || j >= len(grid[i]) || grid[i][j] == '0' {
		return 0
	}

	grid[i][j] = '0'
	dfs(grid, i+1, j)
	dfs(grid, i-1, j)
	dfs(grid, i, j+1)
	dfs(grid, i, j-1)
	return 1
}

func main() {
	// map1 := [][]byte{
	// 	{'1', '1', '1', '1', '0'},
	// 	{'1', '1', '0', '1', '0'},
	// 	{'1', '1', '0', '0', '0'},
	// 	{'0', '0', '0', '0', '0'},
	// }
	map3 := [][]byte{
		{'1', '1', '0', '0', '0'},
		{'1', '1', '0', '0', '0'},
		{'0', '0', '1', '0', '0'},
		{'0', '0', '0', '1', '1'},
	}
	fmt.Println(numIslands(map3))
}
{{< / highlight >}}
</div>
</div>
