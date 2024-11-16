# [136. Single Number](https://leetcode.com/problems/single-number)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

**Example 1:**
> Input: nums = [2,2,1]  
> Output: 1

**Example 2:**
> Input: nums = [4,1,2,1,2]  
> Output: 4

**Example 3:**
> Input: nums = [1]  
> Output: 1

### Constraints:

- Each element in the array appears twice except for one element which appears only once.

---

## My Code

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for num in nums:
            res ^= num
        return res
```

## Explanation

> - The problem asks us to find the single number in an array where every other number appears twice. We use the bitwise XOR (^) operator to solve this efficiently in O(n)O(n) time complexity and with constant space.
> - XOR has the property that a number XORed with itself is 0, and any number XORed with 0 remains unchanged.