---
weight: 460
title: "460 LFU Cache"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_hash_table", "lc_ordered_dict", "lc_ood"]
---

Design and implement a data structure for a [Least Frequently Used (LFU)](https://en.wikipedia.org/wiki/Least_frequently_used) cache.

Implement the `LFUCache` class:

- `LFUCache(int capacity)` Initializes the object with the `capacity` of the data structure.
- `int get(int key)` Gets the value of the `key` if the `key` exists in the cache. Otherwise, returns `-1`.
- `void put(int key, int value)` Update the value of the `key` if present, or inserts the `key` if not already present. When the cache reaches its `capacity`, it should invalidate and remove the **least frequently used** key before inserting a new item. For this problem, when there is a **tie** (i.e., two or more keys with the same frequency), the **least recently used** `key` would be invalidated.

To determine the least frequently used key, a **use counter** is maintained for each key in the cache. The key with the smallest **use counter** is the least frequently used key.

When a key is first inserted into the cache, its **use counter** is set to `1` (due to the put operation). The **use counter** for a key in the cache is incremented either a `get` or `put` operation is called on it.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**
```
Input
["LFUCache", "put", "put", "get", "put", "get", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [3], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, 3, null, -1, 3, 4]

Explanation
// cnt(x) = the use counter for key x
// cache=[] will show the last used order for tiebreakers (leftmost element is  most recent)
LFUCache lfu = new LFUCache(2);
lfu.put(1, 1);   // cache=[1,_], cnt(1)=1
lfu.put(2, 2);   // cache=[2,1], cnt(2)=1, cnt(1)=1
lfu.get(1);      // return 1
                 // cache=[1,2], cnt(2)=1, cnt(1)=2
lfu.put(3, 3);   // 2 is the LFU key because cnt(2)=1 is the smallest, invalidate 2.
                 // cache=[3,1], cnt(3)=1, cnt(1)=2
lfu.get(2);      // return -1 (not found)
lfu.get(3);      // return 3
                 // cache=[3,1], cnt(3)=2, cnt(1)=2
lfu.put(4, 4);   // Both 1 and 3 have the same cnt, but 1 is LRU, invalidate 1.
                 // cache=[4,3], cnt(4)=1, cnt(3)=2
lfu.get(1);      // return -1 (not found)
lfu.get(3);      // return 3
                 // cache=[3,4], cnt(4)=1, cnt(3)=3
lfu.get(4);      // return 4
                 // cache=[4,3], cnt(4)=2, cnt(3)=3
```

**Constraints:**
- <code>0 <= capacity <= 10<sup>4</sup></code>
- <code>0 <= key <= 10<sup>5</sup></code>
- <code>0 <= value <= 10<sup>9</sup></code>
- At most <code>2 * 10<sup>5</sup></code> calls will be made to `get` and `put`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import OrderedDict

class LFUCache:

    def __init__(self, capacity: int):
        self.key_val = {}
        self.key_freq = {}
        self.freq_keys = {}
        self.cap = capacity
        self.min_freq = 0

    def get(self, key: int) -> int:
        if key not in self.key_val:
            return -1
        self._increase_freq(key)
        return self.key_val[key]

    def put(self, key: int, value: int) -> None:
        if self.cap <= 0:
            return
        
        if key in self.key_val:
            self.key_val[key] = value
            self._increase_freq(key)
            return
        
        if self.cap <= len(self.key_val):
            self._remove_min_freq()
        
        self.key_val[key] = value
        self.key_freq[key] = 1
        self.freq_keys.setdefault(1, OrderedDict()).update({key: None})
        self.min_freq = 1
        
    def _increase_freq(self, key: int) -> None:
        freq = self.key_freq[key]
        self.key_freq[key] = freq + 1
        del self.freq_keys[freq][key]
        self.freq_keys.setdefault(freq+1, OrderedDict()).update({key: None})
        if not self.freq_keys[freq]:
            del self.freq_keys[freq]
            if freq == self.min_freq:
                self.min_freq += 1
    
    def _remove_min_freq(self) -> None:
        ordered_key_dict = self.freq_keys[self.min_freq]
        del_key, _ = ordered_key_dict.popitem(last=False)
        if not ordered_key_dict:
            del self.freq_keys[self.min_freq]
        del self.key_val[del_key]
        del self.key_freq[del_key]
        

# Your LFUCache object will be instantiated and called as such:
# obj = LFUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
{{< / highlight >}}
</div>
</div>
