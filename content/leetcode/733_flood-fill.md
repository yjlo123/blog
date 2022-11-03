---
weight: 733
title: "733 Flood Fill"
date: 2021-09-23T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_dfs", "lc_bfs"]
---

An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `newColor`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `newColor`.

Return _the modified image after performing the flood fill_.

**Example 1:**
```
1 1 1      2 2 2
1 1 0  =>  2 2 0
1 0 1      2 0 1

Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, newColor = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.
```

**Example 2:**
```
Input: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, newColor = 2
Output: [[2,2,2],[2,2,2]]
```

**Constraints:**
- `m == image.length`
- `n == image[i].length`
- `1 <= m, n <= 50`
- <code>0 <= image[i][j], newColor < 2<sup>16</sup></code>
- `0 <= sr < m`
- `0 <= sc < n`

> Get the starting pixel color and do BFS.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# === DFS ===
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        color = image[sr][sc]
        if color == newColor:
            return image
        stack = [(sr, sc)]
        while stack:
            r, c = stack.pop()
            if image[r][c] == color:
                image[r][c] = newColor
                if r > 0:
                    stack.append((r-1, c))
                if r < len(image) - 1:
                    stack.append((r+1, c))
                if c > 0:
                    stack.append((r, c-1))
                if c < len(image[0]) - 1:
                    stack.append((r, c+1))
        return image

# === BFS ===
from collections import deque

class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        c = image[sr][sc]
        if c == newColor:
            return image
        image[sr][sc] = newColor
        q = deque([(sr, sc)])
        while q:
            p = q.popleft()
            if p[0] > 0:
                if image[p[0]-1][p[1]] == c:
                    image[p[0]-1][p[1]] = newColor
                    q.append((p[0] - 1, p[1]))
            if p[0] < len(image) - 1:
                if image[p[0]+1][p[1]] == c:
                    image[p[0]+1][p[1]] = newColor
                    q.append((p[0] + 1, p[1]))
            if p[1] < len(image[0]) - 1:
                if image[p[0]][p[1]+1] == c:
                    image[p[0]][p[1]+1] = newColor
                    q.append((p[0], p[1]+1))
            if p[1] > 0:
                if image[p[0]][p[1]-1] == c:
                    image[p[0]][p[1]-1] = newColor
                    q.append((p[0], p[1]-1))
            print(q)
        return image
{{< / highlight >}}
</div>
</div>
