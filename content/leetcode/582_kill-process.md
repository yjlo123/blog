---
weight: 582
title: "582 Kill Process"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bfs", "lc_hash_table"]
---

You have `n` processes forming a rooted tree structure. You are given two integer arrays `pid` and `ppid`, where `pid[i]` is the ID of the ith process and `ppid[i]` is the ID of the <code>i<sup>th</sup></code> process's parent process.

Each process has only **one parent process** but may have multiple children processes. Only one process has `ppid[i] = 0`, which means this process has **no parent process** (the root of the tree).

When a process is **killed**, all of its children processes will also be killed.

Given an integer `kill` representing the ID of a process you want to kill, return _a list of the IDs of the processes that will be killed. You may return the answer in **any order**_.

**Example 1:**
```
  3
 / \
1  (5)
   /
 (10)

Input: pid = [1,3,10,5], ppid = [3,0,5,3], kill = 5
Output: [5,10]
Explanation: The processes colored in red are the processes that should be killed.
```
**Example 2:**
```
Input: pid = [1], ppid = [0], kill = 1
Output: [1]
```

**Constraints:**
- `n == pid.length`
- `n == ppid.length`
- <code>1 <= n <= 5 * 10<sup>4</sup></code>
- <code>1 <= pid[i] <= 5 * 10<sup>4</sup></code>
- <code>0 <= ppid[i] <= 5 * 10<sup>4</sup></code>
- Only one process has no parent.
- All the values of `pid` are **unique**.
- `kill` is **guaranteed** to be in `pid`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def killProcess(
        self,
        pid: List[int],
        ppid: List[int],
        kill: int
    ) -> List[int]:
        child_dict = defaultdict(list)
        for i, p in enumerate(pid):
            child_dict[ppid[i]].append(p)
        q = collections.deque()
        q.append(kill)
        res = []
        while q:
            parent = q.popleft()
            res.append(parent)
            q.extend(child_dict[parent])
        return res
{{< / highlight >}}
</div>
</div>
