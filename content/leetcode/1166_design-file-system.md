---
weight: 1166
title: "1166 Design File System"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_trie"]
---

You are asked to design a file system that allows you to create new paths and associate them with different values.

The format of a path is one or more concatenated strings of the form: `/`followed by one or more lowercase English letters. For example, `"/leetcode"` and `"/leetcode/problems"` are valid paths while an empty string `""` and `"/"` are not.

Implement the `FileSystem` class:
- `bool createPath(string path, int value)` Creates a new `path` and associates a `value` to it if possible and returns `true`. Returns `false` if the path **already exists** or its parent path **doesn't exist**.
- `int get(string path)` Returns the value associated with `path` or returns `-1` if the path doesn't exist.

**Example 1:**
```
Input: 
["FileSystem","createPath","get"]
[[],["/a",1],["/a"]]
Output: 
[null,true,1]
Explanation: 
FileSystem fileSystem = new FileSystem();

fileSystem.createPath("/a", 1); // return true
fileSystem.get("/a"); // return 1
```
**Example 2:**
```
Input: 
["FileSystem","createPath","createPath","get","createPath","get"]
[[],["/leet",1],["/leet/code",2],["/leet/code"],["/c/d",1],["/c"]]
Output: 
[null,true,true,2,false,-1]
Explanation: 
FileSystem fileSystem = new FileSystem();

fileSystem.createPath("/leet", 1); // return true
fileSystem.createPath("/leet/code", 2); // return true
fileSystem.get("/leet/code"); // return 2
fileSystem.createPath("/c/d", 1); // return false because the parent path "/c" doesn't exist.
fileSystem.get("/c"); // return -1 because this path doesn't exist.
```

**Constraints:**
- `2 <= path.length <= 100`
- <code>1 <= value <= 10<sup>9</sup></code>
- Each `path` is valid and consists of lowercase English letters and `'/'`.
- At most <code>10<sup>4</sup></code> calls in total will be made to `createPath` and `get`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class FileSystem:

    def __init__(self):
        self.root = {}

    def createPath(self, path: str, value: int) -> bool:
        cur = self.root
        folders = [i for i in path.split('/') if i]
        for i, p in enumerate(folders):
            if i == len(folders) - 1:
                if p in cur:
                    # path already exists
                    return False
                cur[p] = {'#': value}
                return True
            if p not in cur:
                # parent path doesn't exist
                return False
            cur = cur[p]

    def get(self, path: str) -> int:
        cur = self.root
        for p in [i for i in path.split('/') if i]:
            if p not in cur:
                return -1
            cur = cur[p]
        return cur['#']


# Your FileSystem object will be instantiated and called as such:
# obj = FileSystem()
# param_1 = obj.createPath(path,value)
# param_2 = obj.get(path)
{{< / highlight >}}
</div>
</div>
