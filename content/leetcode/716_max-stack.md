---
weight: 716
title: "716 Max Stack"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_stack", "lc_ood", "lc_heap"]
---

Design a max stack data structure that supports the stack operations and supports finding the stack's maximum element.

Implement the `MaxStack` class:
- `MaxStack()` Initializes the stack object.
- `void push(int x)` Pushes element `x` onto the stack.
- `int pop()` Removes the element on top of the stack and returns it.
- `int top()` Gets the element on the top of the stack without removing it.
- `int peekMax()` Retrieves the maximum element in the stack without removing it.
- `int popMax()` Retrieves the maximum element in the stack and removes it. If there is more than one maximum element, only remove the **top-most** one.

You must come up with a solution that supports `O(1)` for each `top` call and `O(logn)` for each other call.

**Example 1:**
```
Input
["MaxStack", "push", "push", "push", "top", "popMax", "top", "peekMax", "pop", "top"]
[[], [5], [1], [5], [], [], [], [], [], []]
Output
[null, null, null, null, 5, 5, 1, 5, 1, 5]

Explanation
MaxStack stk = new MaxStack();
stk.push(5);   // [5] the top of the stack and the maximum number is 5.
stk.push(1);   // [5, 1] the top of the stack is 1, but the maximum is 5.
stk.push(5);   // [5, 1, 5] the top of the stack is 5, which is also the maximum, because it is the top most one.
stk.top();     // return 5, [5, 1, 5] the stack did not change.
stk.popMax();  // return 5, [5, 1] the stack is changed now, and the top is different from the max.
stk.top();     // return 1, [5, 1] the stack did not change.
stk.peekMax(); // return 5, [5, 1] the stack did not change.
stk.pop();     // return 1, [5] the top of the stack and the max element is now 5.
stk.top();     // return 5, [5] the stack did not change.
```

**Constraints:**
- <code>-10<sup>7</sup> <= x <= 10<sup>7</sup></code>
- At most <code>10<sup>5</sup></code> calls will be made to `push`, `pop`, `top`, `peekMax`, and `popMax`.
- There will be **at least one element** in the stack when pop, top, peekMax, or popMax is called.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class MaxStack:

    def __init__(self):
        self.deleted = set()
        self.cur_id = 0
        self.stack = []
        self.heap = []

    def push(self, x: int) -> None:
        new_id= self.cur_id
        self.cur_id += 1
        self.stack.append((x, new_id))
        heapq.heappush(self.heap, (-x, -new_id))

    def pop(self) -> int:
        while self.stack and self.stack[-1][1] in self.deleted:
            self.stack.pop()
        val, eid = self.stack.pop()
        self.deleted.add(eid)
        return val

    def top(self) -> int:
        while self.stack and self.stack[-1][1] in self.deleted:
            self.stack.pop()
        return self.stack[-1][0]

    def peekMax(self) -> int:
        while self.heap and -self.heap[0][1] in self.deleted:
            heapq.heappop(self.heap)
        return -self.heap[0][0]

    def popMax(self) -> int:
        while self.heap and -self.heap[0][1] in self.deleted:
            heapq.heappop(self.heap)
        val, eid = heapq.heappop(self.heap)
        self.deleted.add(-eid)
        return -val


# Your MaxStack object will be instantiated and called as such:
# obj = MaxStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.peekMax()
# param_5 = obj.popMax()
{{< / highlight >}}
</div>
</div>
