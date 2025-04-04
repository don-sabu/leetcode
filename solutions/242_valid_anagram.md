# [242. Valid Anagram](https://leetcode.com/problems/valid-anagram)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

> **Example 1:**
>
> Input: s = "anagram", t = "nagaram"  
> Output: true  
>
> **Example 2:**
>
> Input: s = "rat", t = "car"  
> Output: false  

### Constraints:
- `1 <= s.length, t.length <= 5 * 10^4`
- `s` and `t` consist of lowercase English letters.

## My Code

```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```

## Explanation

To check whether two strings are anagrams, we need to verify that both have the same characters with the same frequency. Python's `collections.Counter` efficiently counts the occurrences of each character in both strings. If the resulting dictionaries are equal, the strings are anagrams of each other. This approach runs in linear time, `O(n)`, where `n` is the length of the strings.

