# [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

> **Example 1:**  
> **Input:** nums = [1,2,3,1]  
> **Output:** true  
> **Explanation:** The element 1 occurs at the indices 0 and 3.

> **Example 2:**  
> **Input:** nums = [1,2,3,4]  
> **Output:** false  
> **Explanation:** All elements are distinct.

> **Example 3:**  
> **Input:** nums = [1,1,1,3,3,4,3,2,4,2]  
> **Output:** true  

### Constraints:
- 1 <= nums.length <= 10^5
- -10^9 <= nums[i] <= 10^9

## Solution
```python
from typing import List

class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(set(nums)) != len(nums)
```

## Explanation
This solution utilizes a **set**, which only stores unique elements. By converting the list `nums` into a set, all duplicate values are removed. If the length of the set is **smaller** than the original list, it means that duplicates were present. If the lengths are equal, it means all elements were distinct. The solution runs in **O(n)** time complexity and requires **O(n)** extra space.

