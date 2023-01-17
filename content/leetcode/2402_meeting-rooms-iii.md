---
weight: 2402
title: "2402 Meeting Rooms III"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_heap"]
---

You are given an integer `n`. There are `n` rooms numbered from `0` to `n - 1`.

You are given a 2D integer array `meetings` where <code>meetings[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> means that a meeting will be held during the half-closed time interval <code>[start<sub>i</sub>, end<sub>i</sub>)</code>. All the values of <code>start<sub>i</sub></code> are **unique**.

Meetings are allocated to rooms in the following manner:

Each meeting will take place in the unused room with the **lowest** number.
If there are no available rooms, the meeting will be delayed until a room becomes free. The delayed meeting should have the **same** duration as the original meeting.
When a room becomes unused, meetings that have an earlier original **start** time should be given the room.
Return _the **number** of the room that held the most meetings. If there are multiple rooms, return the room with the **lowest** number_.

A **half-closed interval** `[a, b)` is the interval between `a` and `b` **including** a and **not including** `b`.

**Example 1:**
```
Input: n = 2, meetings = [[0,10],[1,5],[2,7],[3,4]]
Output: 0
Explanation:
- At time 0, both rooms are not being used. The first meeting starts in room 0.
- At time 1, only room 1 is not being used. The second meeting starts in room 1.
- At time 2, both rooms are being used. The third meeting is delayed.
- At time 3, both rooms are being used. The fourth meeting is delayed.
- At time 5, the meeting in room 1 finishes. The third meeting starts in room 1 for the time period [5,10).
- At time 10, the meetings in both rooms finish. The fourth meeting starts in room 0 for the time period [10,11).
Both rooms 0 and 1 held 2 meetings, so we return 0. 
```
**Example 2:**
```
Input: n = 3, meetings = [[1,20],[2,10],[3,5],[4,9],[6,8]]
Output: 1
Explanation:
- At time 1, all three rooms are not being used. The first meeting starts in room 0.
- At time 2, rooms 1 and 2 are not being used. The second meeting starts in room 1.
- At time 3, only room 2 is not being used. The third meeting starts in room 2.
- At time 4, all three rooms are being used. The fourth meeting is delayed.
- At time 5, the meeting in room 2 finishes. The fourth meeting starts in room 2 for the time period [5,10).
- At time 6, all three rooms are being used. The fifth meeting is delayed.
- At time 10, the meetings in rooms 1 and 2 finish. The fifth meeting starts in room 1 for the time period [10,12).
Room 0 held 1 meeting while rooms 1 and 2 each held 2 meetings, so we return 1. 
```

**Constraints:**
- `1 <= n <= 100`
- <code>1 <= meetings.length <= 10<sup>5</sup></code>
- `meetings[i].length == 2`
- <code>0 <= start<sub>i</sub> < end<sub>i</sub> <= 5 * 10<sup>5</sup></code>
- All the values of <code>start<sub>i</sub></code> are **unique**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    
    def mostBooked(self, n: int, meetings: List[List[int]]) -> int:
        room_count = [0] * n
        avail_rooms = [i for i in range(n)] # heap of room_id
        heapq.heapify(avail_rooms)

        current_meetings = []  # min heap: (end_time, room_id)
        delayed_meetings = deque([])  # (duration)
        pending_meetings = deque(sorted(meetings))  # (start, end)

        while pending_meetings or delayed_meetings:
            # == process delayed meeting
            if delayed_meetings:
                delay_meeting_duration = delayed_meetings.popleft()
                end_time, room_id = heapq.heappop(current_meetings)
                room_count[room_id] += 1
                heapq.heappush(
                    current_meetings,
                    (end_time + delay_meeting_duration, room_id)
                )
                continue

            # == process pending meeting
            start, end = pending_meetings.popleft()

            # release rooms
            while current_meetings and current_meetings[0][0] <= start:
                _, released_room_id = heapq.heappop(current_meetings)
                heapq.heappush(avail_rooms, released_room_id)
            
            if not avail_rooms:
                # all rooms being used
                delayed_meetings.append(end - start)
            else:
                room_id = heapq.heappop(avail_rooms)
                heapq.heappush(current_meetings, (end, room_id))
                room_count[room_id] += 1

        return room_count.index(max(room_count))


'''
Simpler Version
'''
class Solution:
    
    def mostBooked(self, n: int, meetings: List[List[int]]) -> int:
        room_count = [0] * n
        avail_rooms = [i for i in range(n)] # heap of room_id
        heapq.heapify(avail_rooms)

        current_meetings = []  # min heap: (end_time, room_id)

        for start, end in sorted(meetings):
            while current_meetings and current_meetings[0][0] <= start:
                end_time, room_id = heapq.heappop(current_meetings)
                heapq.heappush(avail_rooms, room_id)

            if avail_rooms:
                room_id = heapq.heappop(avail_rooms)
                heapq.heappush(
                    current_meetings,
                    (end, room_id)
                )
            else:
                end_time, room_id = heapq.heappop(current_meetings)
                heapq.heappush(
                    current_meetings,
                    (end_time + end - start, room_id)
                )
            room_count[room_id] += 1

        return room_count.index(max(room_count))
{{< / highlight >}}
</div>
</div>