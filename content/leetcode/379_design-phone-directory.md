---
weight: 379
title: "379 Design Phone Directory"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_ood", "lc_queue"]
---

Design a phone directory that initially has `maxNumbers` empty slots that can store numbers. The directory should store numbers, check if a certain slot is empty or not, and empty a given slot.

Implement the `PhoneDirectory` class:
- `PhoneDirectory(int maxNumbers)` Initializes the phone directory with the number of available slots `maxNumbers`.
- `int get()` Provides a number that is not assigned to anyone. Returns `-1` if no number is available.
- `bool check(int number)` Returns `true` if the slot `number` is available and `false` otherwise.
- `void release(int number)` Recycles or releases the slot `number`.

**Example 1:**
```
Input
["PhoneDirectory", "get", "get", "check", "get", "check", "release", "check"]
[[3], [], [], [2], [], [2], [2], [2]]
Output
[null, 0, 1, true, 2, false, null, true]

Explanation
PhoneDirectory phoneDirectory = new PhoneDirectory(3);
phoneDirectory.get();      // It can return any available phone number. Here we assume it returns 0.
phoneDirectory.get();      // Assume it returns 1.
phoneDirectory.check(2);   // The number 2 is available, so return true.
phoneDirectory.get();      // It returns 2, the only number that is left.
phoneDirectory.check(2);   // The number 2 is no longer available, so return false.
phoneDirectory.release(2); // Release number 2 back to the pool.
phoneDirectory.check(2);   // Number 2 is available again, return true.
```

**Constraints:**
- <code>1 <= maxNumbers <= 10<sup>4</sup></code>
- `0 <= number < maxNumbers`
- At most <code>2 * 10<sup>4</sup></code> calls will be made to `get`, `check`, and `release`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
'''
Using Set
'''
class PhoneDirectory:

    def __init__(self, maxNumbers: int):
        self.avail_set = {i for i in range(maxNumbers)}

    def get(self) -> int:
        if not self.avail_set:
            return -1
        return self.avail_set.pop()

    def check(self, number: int) -> bool:
        return number in self.avail_set

    def release(self, number: int) -> None:
        self.avail_set.add(number)


# Your PhoneDirectory object will be instantiated and called as such:
# obj = PhoneDirectory(maxNumbers)
# param_1 = obj.get()
# param_2 = obj.check(number)
# obj.release(number)


'''
Using pointers

Use an array slots[] to store the next available number.
- when a number k is issued, move pointer pos = slots[k] to the next
  available position. set slots[k]=-1 and
- when a number is recycled, sipmly move pointer from pos to the
  recycled number, and change the recycled number's "next" point to pos.
'''
class PhoneDirectory:

    def __init__(self, maxNumbers: int):
        # slots of next pointers
        self.slots = [(i + 1) % maxNumbers for i in range(maxNumbers)]
        self.pos = 0

    def get(self) -> int:
        if self.slots[self.pos] == -1:
            return -1
        ret = self.pos
        self.pos = self.slots[self.pos]
        self.slots[ret] = -1
        return ret

    def check(self, number: int) -> bool:
        return self.slots[number] != -1

    def release(self, number: int) -> None:
        if self.slots[number] != -1:
            # slot is avail
            return
        self.slots[number] = self.pos
        self.pos = number
{{< / highlight >}}
</div>
</div>
