---
weight: 118
title: "118 Pascal's Triangle"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array", "lc_dp"]
---

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

```
    1
   1 1
  1 2 1
 1 3 3 1
1 4 6 4 1
```

**Example 1:**
```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```
**Example 2:**
```
Input: numRows = 1
Output: [[1]]
```

**Constraints:**
- 1 <= numRows <= 30

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def __init__(self):
        self.rows = [[1]]
        for i in range(29):
            prev_now = self.rows[-1]
            new_row = [prev_now[0]]
            for i in range(1, len(prev_now)):
                new_row.append(prev_now[i-1] + prev_now[i])
            new_row.append(prev_now[-1])
            self.rows.append(new_row)
    
    def generate(self, numRows: int) -> List[List[int]]:
        return self.rows[:numRows]
{{< / highlight >}}
</div>
</div>
