# [704. Binary Search](https://leetcode.com/problems/binary-search/)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

> **Example 1:**  
> Input: nums = [-1,0,3,5,9,12], target = 9  
> Output: 4  
> Explanation: 9 exists in nums and its index is 4

> **Example 2:**  
> Input: nums = [-1,0,3,5,9,12], target = 2  
> Output: -1  
> Explanation: 2 does not exist in nums so return -1

### Constraints:
- 1 <= nums.length <= 10⁴  
- -10⁴ < nums[i], target < 10⁴  
- All the integers in `nums` are unique  
- `nums` is sorted in ascending order

---

## My Code

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if target == nums[mid]:
                return mid
            elif target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        return -1
```

---

## Explanation

This is a classic binary search implementation. The idea is to repeatedly divide the search interval in half. We initialize two pointers, `left` and `right`, representing the current search bounds. In each iteration, we calculate the midpoint and check whether the target value is equal to the middle element. If it is, we return the index. If the target is smaller, we discard the right half, otherwise, we discard the left half. This process continues until the bounds overlap, ensuring O(log n) time complexity.
