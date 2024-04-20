---
title: "Python Algorithm Cheatsheet"
date: 2024-04-20T00:00:00-04:00
draft: false
tags: ["programming language", "algorithm"]
---

## List

### new list
``` python
lst = []
```

### methods
``` python
lst.append(3)
lst.extend([5, 6])
last = lst.pop()      # last element is removed
count = lst.count(2)  # number of elements equal to 2
lst.sort(reverse=True)
```

### others
``` python
# concatenate
[1, 2] + [3, 4]
```

### slicing
``` python
lst[3:6] # from index 3 (included) to index 6 (not included)
lst[:4]  # from start to index 4 (not included)
lst[3:]  # from index 3 (included) to the end
lst[:]   # copy of the list
lst[:-1] # from start to the second last (included)
```

### built-in functions for array
