---
weight: 1
title: "1 Two Sum"
date: 2020-09-21T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_hash_table"]
---



Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to _`target`_.

You may assume that each input would have _**exactly**_ **one solution**, and you may not use the same element twice.

You can return the answer in any order.

**Example 1:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

**Constraints:**
* <code>2 <= nums.length <= 10<sup>5</sup></code>
* <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
* <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>
* **Only one valid answer exists.**

**Follow-up:** Can you come up with an algorithm that is less than <code>O(n<sup>2</sup>)</code> time complexity?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
def twoSum(nums: 'List[int]', target: 'int') -> 'List[int]':
    map = {}
    for i, n in enumerate(nums):
        if n in map:
            return [map[n], i]
        map[target-n] = i
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func twoSum(nums []int, target int) []int {
    d := make(map[int]int)
    for idx, num := range nums {
        if v, ok := d[num]; ok {
            return []int{v, idx}
        }
        d[target-num] = idx
    }
    return nil
}
{{< / highlight >}}
</div>

<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int comp = target - nums[i];
        if (map.containsKey(comp)) {
            return new int[]{map.get(comp), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
{{< / highlight >}}
</div>

<div id="kotlin" class="lang">
{{< highlight kotlin "linenos=table" >}}
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        val diffMap = mutableMapOf<Int, Int>()
        nums.forEachIndexed { i, num ->
            diffMap[num]?.let {
                return intArrayOf(it, i)
            }
            diffMap[target - num] = i
        }
        return intArrayOf()
    }
}
{{< / highlight >}}
</div>

<div id="c++" class="lang">
{{< highlight cpp "linenos=table" >}}
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> imap;

    for (int i = 0;; ++i) {
        auto it = imap.find(target - nums[i]);

        if (it != imap.end()) 
            return vector<int> {i, it->second};

        imap[nums[i]] = i;
    }
}
{{< / highlight >}}
</div>

<div id="swift" class="lang">
{{< highlight swift "linenos=table" >}}
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var dict = [Int: Int]()

        for (index, value) in nums.enumerated() {
          if let i = dict[value] {
            return [i, index]
          } else {
            dict[target - value] = index
          }
        }

        return []
    }
}
{{< / highlight >}}
</div>

<div id="rust" class="lang">
{{< highlight rust "linenos=table" >}}
pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
    use std::collections::HashMap;
    
    let mut m: HashMap<i32, i32> = HashMap::new();
    for (i, v) in nums.iter().enumerate() {
        match m.get(&(target - *v)) {
            Some(&i2) => return vec![i as i32, i2],
            None => m.insert(*v, i as i32),
        };
    }
    vec![]
}
{{< / highlight >}}
</div>

<div id="javascript" class="lang">
{{< highlight javascript "linenos=table" >}}
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let map = {};

    for (let i = 0; i < nums.length; i++) {
      const comp = target - nums[i];
      if (map[comp] !== undefined) {
        return [map[comp], i]
      }
      map[nums[i]] = i
    }

    return []
};
{{< / highlight >}}
</div>

<div id="runtime" class="lang">
    <div class="code-link">
        <div class="runtime-embedded-box" style="width: 100%; height: 420px;">let input []
psh $input 2 7 11 15
cal two_sum $input 22
prt $ret
<pre></pre>
def two_sum
 let _list $0
 let _target $1
 let _result []
 let _map {}
 let _idx 0
 <pre></pre>
 for _num $_list
  get $_map $_num _v
  ife $_v $nil
   sub _key $_target $_num
   put $_map $_key $_idx
  els
   psh $_result $_v $_idx
   ret $_result
  fin
  add _idx $_idx 1
 nxt
 ret $_result
end
        </div>
    </div>
</div>
</div>
