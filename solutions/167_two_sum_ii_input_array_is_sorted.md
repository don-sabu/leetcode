# [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.

> **Example 1:**
>
> Input: numbers = [2,7,11,15], target = 9  
> Output: [1,2]  
> Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].  
>
> **Example 2:**
>
> Input: numbers = [2,3,4], target = 6  
> Output: [1,3]  
> Explanation: The sum of 2 and 4 is 6. Therefore, index1 = 1, index2 = 3. We return [1, 3].  
>
> **Example 3:**
>
> Input: numbers = [-1,0], target = -1  
> Output: [1,2]  
> Explanation: The sum of -1 and 0 is -1. Therefore, index1 = 1, index2 = 2. We return [1, 2].  

### Constraints:
- `2 <= numbers.length <= 3 * 10^4`
- `-1000 <= numbers[i] <= 1000`
- `numbers` is sorted in non-decreasing order.
- `-1000 <= target <= 1000`
- The tests are generated such that there is exactly one solution.

## My Code

```python
from typing import List

class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        i = 0
        j = len(numbers) - 1
        while i < j:
            s = numbers[i] + numbers[j]
            if s == target:
                return [i+1, j+1]
            elif s < target:
                i += 1
            else:
                j -= 1
```

## Explanation

The given array is sorted in non-decreasing order, so we can use the two-pointer technique to solve this problem efficiently in O(n) time complexity.

- We initialize two pointers: `i` at the beginning (index 0) and `j` at the end (index `len(numbers) - 1`).
- We calculate the sum of `numbers[i]` and `numbers[j]`.
- If the sum equals the target, we return the 1-based indices `[i+1, j+1]`.
- If the sum is less than the target, we move the left pointer `i` one step forward to increase the sum.
- If the sum is greater than the target, we move the right pointer `j` one step backward to decrease the sum.
- Since there is exactly one solution, we are guaranteed to find the answer.

This approach ensures that we use constant extra space and efficiently find the solution in a sorted array.

