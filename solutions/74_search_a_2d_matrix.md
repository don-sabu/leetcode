# [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if `target` is in the matrix or `false` otherwise.

You must write a solution in O(log(m * n)) time complexity.

> **Example 1:**  
> Input:  
> matrix =  
> \[
>   [1, 3, 5, 7],  
>   [10, 11, 16, 20],  
>   [23, 30, 34, 60]  
> \], 
> target = 3  
> Output: `true`

> **Example 2:**  
> Input:  
> matrix =  
> \[
>   [1, 3, 5, 7],  
>   [10, 11, 16, 20],  
>   [23, 30, 34, 60]  
> \], 
> target = 13  
> Output: `false`

### Constraints:
- `m == matrix.length`  
- `n == matrix[i].length`  
- `1 <= m, n <= 100`  
- `-10⁴ <= matrix[i][j], target <= 10⁴`

---

## My Code

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        r = len(matrix)
        c = len(matrix[0])
        left = 0
        right = r * c - 1
        while left <= right:
            mid = (left + right) // 2
            mid_r = mid // c
            mid_c = mid % c
            if target == matrix[mid_r][mid_c]:
                return True
            elif target < matrix[mid_r][mid_c]:
                right = mid - 1
            else:
                left = mid + 1
        return False
```

---

## Explanation

The key insight is to treat the 2D matrix as a flattened 1D array while preserving its sorted nature. Since each row is sorted and the first element of each row is greater than the last of the previous row, we can perform a binary search over a virtual 1D array of size `m * n`.

We compute the mid index, then convert it back to a 2D index using `row = mid // columns` and `col = mid % columns`. We compare the `matrix[row][col]` with the target and adjust the binary search bounds accordingly. This approach ensures O(log(m * n)) time complexity.
