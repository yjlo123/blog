---
weight: 383
title: "383 Ransom Note"
date: 2021-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

Given two stings `ransomNote` and `magazine`, return _`true` if `ransomNote` can be constructed from `magazine` and `false` otherwise_.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1:**
```
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2:**
```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

**Example 3:**
```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

**Constraints:**
- <code>1 <= ransomNote.length, magazine.length <= 10<sup>5</sup></code>
- `ransomNote` and `magazine` consist of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        for i in set(ransomNote):
            if ransomNote.count(i) > magazine.count(i):
                return False
        return True
{{< / highlight >}}
</div>

<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
public class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] count = new int[26];
        char[] mag = magazine.toCharArray();
        for(char c : mag){
            count[c-'a']++;
        }
        
        char[] ran = ransomNote.toCharArray();
        for(char r : ran){
            if(--count[r-'a'] < 0) return false;
        }
        return true;
    }
}
{{< / highlight >}}
</div>
</div>
