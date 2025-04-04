# [49. Group Anagrams](https://leetcode.com/problems/group-anagrams)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

> **Example 1:**
>
> Input: strs = ["eat","tea","tan","ate","nat","bat"]  
> Output: [["bat"],["nat","tan"],["ate","eat","tea"]]  
>
> **Example 2:**
>
> Input: strs = [""]  
> Output: [[""]]  
>
> **Example 3:**
>
> Input: strs = ["a"]  
> Output: [["a"]]  

### Constraints:
- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

## My Code

### Solution 1 (Sorting Approach)
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        group = defaultdict(list)

        for s in strs:
            group["".join(sorted(s))].append(s)
        
        return list(group.values())
```

### Solution 2 (Frequency Count Approach)
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        group = defaultdict(list)

        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c)-ord('a')] += 1
            group[tuple(count)].append(s)
        
        return list(group.values())
```

## Explanation

The problem requires us to group words that are anagrams. We solve this using two approaches:

1. **Sorting Approach:**
   - We sort each word alphabetically and use the sorted word as a key in a dictionary.
   - All words that share the same sorted form are grouped together.
   - Sorting takes `O(k log k)` for each word (where `k` is the word length), making the total complexity `O(n k log k)`.

2. **Frequency Count Approach:**
   - Instead of sorting, we use a frequency count of letters as the key.
   - Each word is represented as a tuple of 26 integers (one per letter from 'a' to 'z').
   - This avoids sorting, reducing complexity to `O(nk)`, making it more efficient for long words.

