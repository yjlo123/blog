---
weight: 895
title: "895 Maximum Frequency Stack"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_hash_table", "lc_stack"]
---

Design a stack-like data structure to push elements to the stack and pop the most frequent element from the stack.

Implement the `FreqStack` class:
- `FreqStack()` constructs an empty frequency stack.
- `void push(int val)` pushes an integer `val` onto the top of the stack.
- `int pop()` removes and returns the most frequent element in the stack.
  - If there is a tie for the most frequent element, the element closest to the stack's top is removed and returned.
 

**Example 1:**
```
Input
["FreqStack", "push", "push", "push", "push", "push", "push", "pop", "pop", "pop", "pop"]
[[], [5], [7], [5], [7], [4], [5], [], [], [], []]
Output
[null, null, null, null, null, null, null, 5, 7, 5, 4]

Explanation
FreqStack freqStack = new FreqStack();
freqStack.push(5); // The stack is [5]
freqStack.push(7); // The stack is [5,7]
freqStack.push(5); // The stack is [5,7,5]
freqStack.push(7); // The stack is [5,7,5,7]
freqStack.push(4); // The stack is [5,7,5,7,4]
freqStack.push(5); // The stack is [5,7,5,7,4,5]
freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,5,7,4].
freqStack.pop();   // return 7, as 5 and 7 is the most frequent, but 7 is closest to the top. The stack becomes [5,7,5,4].
freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,4].
freqStack.pop();   // return 4, as 4, 5 and 7 is the most frequent, but 4 is closest to the top. The stack becomes [5,7].
```

**Constraints:**
- <code>0 <= val <= 10<sup>9</sup></code>
- At most <code>2 * 10<sup>4</sup></code> calls will be made to push and pop.
- It is guaranteed that there will be at least one element in the stack before calling `pop`.

```
Stack of stack

push(5) - { 1:[5] }
push(7) - { 1:[5,7]] }
push(5) - { 1:[5,7]],  2:[5]] }
push(7) - { 1:[5,7]],  2:[5,7] }
push(4) - { 1:[5,7,4], 2:[5,7] }
push(5) - { 1:[5,7,4], 2:[5,7], 3:[5] }
pop()   - { 1:[5,7,4], 2:[5,7] } => 5
pop()   - { 1:[5,7,4], 2:[5] } => 7
pop()   - { 1:[5,7,4] } => 5
pop()   - { 1:[5,7]] } => 4
```


<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class FreqStack:

    def __init__(self):
        self.val_freq = defaultdict(int)
        self.freq_list = defaultdict(list)
        self.max_freq = 0

    def push(self, val: int) -> None:
        self.val_freq[val] += 1
        new_freq = self.val_freq[val]
        if new_freq > self.max_freq:
            self.max_freq = new_freq
        self.freq_list[new_freq].append(val)

    def pop(self) -> int:
        val = self.freq_list[self.max_freq].pop()
        self.val_freq[val] -= 1
        if not self.freq_list[self.max_freq]:
            self.max_freq -= 1
        return val


# Your FreqStack object will be instantiated and called as such:
# obj = FreqStack()
# obj.push(val)
# param_2 = obj.pop()
{{< / highlight >}}
</div>
</div>
