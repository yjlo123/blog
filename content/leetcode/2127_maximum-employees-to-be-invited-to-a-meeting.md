---
weight: 2127
title: "2127 Maximum Employees to Be Invited to a Meeting"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs", "lc_linked_list"]
---

A company is organizing a meeting and has a list of `n` employees, waiting to be invited. They have arranged for a large circular table, capable of seating any number of employees.

The employees are numbered from `0` to `n - 1`. Each employee has a **favorite** person and they will attend the meeting **only if** they can sit next to their favorite person at the table. The favorite person of an employee is **not** themself.

Given a **0-indexed** integer array `favorite`, where `favorite[i]` denotes the favorite person of the <code>i<sup>th</sup></code> employee, return _the **maximum number of employees** that can be invited to the meeting_.

**Example 1:**
```
 2 - 1
  \ /
   0

Input: favorite = [2,2,1,2]
Output: 3
Explanation:
The above figure shows how the company can invite employees 0, 1, and 2, and seat them at the round table.
All employees cannot be invited because employee 2 cannot sit beside employees 0, 1, and 3, simultaneously.
Note that the company can also invite employees 1, 2, and 3, and give them their desired seats.
The maximum number of employees that can be invited to the meeting is 3.
``` 
**Example 2:**
```
Input: favorite = [1,2,0]
Output: 3
Explanation: 
Each employee is the favorite person of at least one other employee, and the only way the company can invite them is if they invite every employee.
The seating arrangement will be the same as that in the figure given in example 1:
- Employee 0 will sit between employees 2 and 1.
- Employee 1 will sit between employees 0 and 2.
- Employee 2 will sit between employees 1 and 0.
The maximum number of employees that can be invited to the meeting is 3.
```
**Example 3:**
```
   4
 /   \
3     1
 \   /
   0

Input: favorite = [3,0,1,4,1]
Output: 4
Explanation:
The above figure shows how the company will invite employees 0, 1, 3, and 4, and seat them at the round table.
Employee 2 cannot be invited because the two spots next to their favorite employee 1 are taken.
So the company leaves them out of the meeting.
The maximum number of employees that can be invited to the meeting is 4.
```

**Constraints:**
- `n == favorite.length`
- <code>2 <= n <= 10<sup>5</sup></code>
- `0 <= favorite[i] <= n - 1`
- `favorite[i] != i`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maximumInvitations(self, favorite: List[int]) -> int:
        followers = defaultdict(set)
        for i, f in enumerate(favorite):
            followers[f].add(i)
        
        available = set(range(len(favorite)))
        sum_chain = 0
        max_circle = 0

        def dfs(a: int, excl: int = None) -> int:
            available.remove(a)
            stack = [
                (b, 1)
                for b in followers[a]
                if b in available and b != excl
            ]
            if not stack:
                return 0
           
            max_len = 1
            while stack:
                cur, n = stack.pop()
                available.remove(cur)
                max_len = max(max_len, n)
                for b in followers[cur]:
                    if b in available:
                        stack.append((b, n+1))
            return max_len

        
        while available:
            a = list(available).pop()
            lst = {a: 1} # node in the linked list and its seq num
            # the linked list must contain a loop
            while favorite[a] not in lst:
                a = favorite[a]
                lst[a] = len(lst) + 1

            circle_size = len(lst) + 1 - lst[favorite[a]]
            if circle_size == 2:
                # Case 1: two mutual favorite with two arms
                sum_chain += 2 + dfs(a, favorite[a]) + dfs(favorite[a], a)
            else:
                # Case 2: a circle of more than two nodes
                max_circle = max(max_circle, circle_size)
                dfs(a) # remove all node of the circle from available
        return max(sum_chain, max_circle)
{{< / highlight >}}
</div>
</div>
