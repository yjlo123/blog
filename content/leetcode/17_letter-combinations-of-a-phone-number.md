---
weight: 17
title: "17 Letter Combinations of a Phone Number"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```
   1       2(abc)  3(def)
   4(ghi)  5(jkl)  6(mno)
   7(pqrs) 8(tuv)  9(wxyz)
   *+      0_      ^#
```

**Example 1:**
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```
**Example 2:**
```
Input: digits = ""
Output: []
```
**Example 3:**
```
Input: digits = "2"
Output: ["a","b","c"]
```

**Constraints:**
- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
        M = [0, 1, 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
        res = ['']
        for c in digits:
            res = [p+n for p in res for n in M[int(c)]]
        return res
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight golang "linenos=table" >}}
func letterCombinations(digits string) []string {
	if digits == "" {
		return []string{}
	}

	m := map[byte]string{
		'0': "0",
		'1': "1",
		'2': "abc",
		'3': "def",
		'4': "ghi",
		'5': "jkl",
		'6': "mno",
		'7': "pqrs",
		'8': "tuv",
		'9': "wxyz",
	}

	var res []string
	backtrack("", &res, 0, digits, m)
	return res
}

func backtrack(cur string, res *[]string, i int, digits string, m map[byte]string) {
	if i == len(digits) {
		*res = append(*res, cur)
		return
	}
	for _, c := range m[digits[i]] {
		backtrack(cur+string(c), res, i+1, digits, m)
	}
}
{{< / highlight >}}
</div>

<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
class Solution {
    public static Map<String, String> M = Map.of(
            "2", "abc",
            "3", "def",
            "4", "ghi",
            "5", "jkl",
            "6", "mno",
            "7", "pqrs",
            "8", "tuv",
            "9", "wxyz");

    public List<String> letterCombinations(String digits) {
        ArrayList<String> res = new ArrayList<>();
        if (digits.length() == 0) {
            return res;
        }
        backtrack("", 0, digits, res);
        return res;
    }

    private void backtrack(String cur, int i, String digits, List<String> res) {
        if (i == digits.length()) {
            res.add(cur);
        } else {
            String chars = M.get(String.valueOf(digits.charAt(i)));
            for (char c : chars.toCharArray()) {
                backtrack(cur+c, i+1, digits, res);
            }
        }
    }
}
{{< / highlight >}}
</div>
</div>
