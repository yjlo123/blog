---
weight: 1606
title: "1606 Find Servers That Handled Most Number of Requests"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_heap"]
---

You have `k` servers numbered from `0` to `k-1` that are being used to handle multiple requests simultaneously. Each server has infinite computational capacity but **cannot handle more than one request at a time**. The requests are assigned to servers according to a specific algorithm:
- The <code>i<sup>th</sup></code> (0-indexed) request arrives.
- If all servers are busy, the request is dropped (not handled at all).
- If the <code>(i % k)<sup>th</sup></code> server is available, assign the request to that server.
- Otherwise, assign the request to the next available server (wrapping around the list of servers and starting from 0 if necessary). For example, if the <code>i<sup>th</sup></code> server is busy, try to assign the request to the <code>(i+1)<sup>th</sup></code> server, then the <code>(i+2)<sup>th</sup></code> server, and so on.

You are given a **strictly increasing** array `arrival` of positive integers, where `arrival[i]` represents the arrival time of the <code>i<sup>th</sup></code> request, and another array `load`, where `load[i]` represents the load of the <code>i<sup>th</sup></code> request (the time it takes to complete). Your goal is to find the **busiest server(s)**. A server is considered **busiest** if it handled the most number of requests successfully among all the servers.

Return *a list containing the IDs (0-indexed) of the **busiest server(s)***. You may return the IDs in any order.

**Example 1:**
```
Dropped                   [R4--L=3----]
Server 2          [R2--L=3----]
Server 1     [R1--L=2-][R3--L=3---]
Server 0  [R0--L=5------------]
          1   2   3   4   5   6   7   8

Input: k = 3, arrival = [1,2,3,4,5], load = [5,2,3,3,3] 
Output: [1] 
Explanation: 
All of the servers start out available.
The first 3 requests are handled by the first 3 servers in order.
Request 3 comes in. Server 0 is busy, so it's assigned to the next available server, which is 1.
Request 4 comes in. It cannot be handled since all servers are busy, so it is dropped.
Servers 0 and 2 handled one request each, while server 1 handled two requests.
Hence server 1 is the busiest server.
```
**Example 2:**
```
Input: k = 3, arrival = [1,2,3,4], load = [1,2,1,2]
Output: [0]
Explanation: 
The first 3 requests are handled by first 3 servers.
Request 3 comes in. It is handled by server 0 since the server is available.
Server 0 handled two requests, while servers 1 and 2 handled one request each.
Hence server 0 is the busiest server.
```
**Example 3:**
```
Input: k = 3, arrival = [1,2,3], load = [10,12,11]
Output: [0,1,2]
Explanation: Each server handles a single request,
so they are all considered the busiest.
```

**Constraints:**
- <code>1 <= k <= 10<sup>5</sup></code>
- <code>1 <= arrival.length, load.length <= 10<sup>5</sup></code>
- `arrival.length == load.length`
- <code>1 <= arrival[i], load[i] <= 10<sup>9</sup></code>
- `arrival` is strictly increasing.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def busiestServers(self, k: int, arrival: List[int], load: List[int]) -> List[int]:
        count = [0] * k
        busy = []  # min heap (end_time, server_id)
        free = list(range(k))  # min heap of free servers
        
        for i, (a, l) in enumerate(zip(arrival, load)):
            while busy and busy[0][0] <= a:
                # release finished servers
                _, server_id = heapq.heappop(busy)
                # make sure idx >= i
                idx = i + (server_id - i) % k
                heapq.heappush(free, idx)

            if not free:
                continue

            busy_id = heapq.heappop(free) % k
            heapq.heappush(busy, (a + l, busy_id))
            count[busy_id] += 1

        max_count = max(count)
        return [i for i, c in enumerate(count) if c == max_count]
{{< / highlight >}}
</div>
</div>
