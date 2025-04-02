# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`th line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

> **Example 1:**
>
> Input: height = [1,8,6,2,5,4,8,3,7]  
> Output: 49  
> Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7].  
> In this case, the max area of water (blue section) the container can contain is 49.  
>
> **Example 2:**
>
> Input: height = [1,1]  
> Output: 1  

### Constraints:
- `n == height.length`
- `2 <= n <= 10^5`
- `0 <= height[i] <= 10^4`

## My Code

```python
from typing import List

class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_area = 0
        i = 0
        j = len(height) - 1
        while i < j:
            area = min(height[i], height[j]) * (j - i)
            if height[i] < height[j]:
                i += 1
            else:
                j -= 1
            max_area = max(area, max_area)
        return max_area
```

## Explanation

The problem requires finding two vertical lines that form a container with the x-axis, maximizing the stored water. The optimal approach uses the **two-pointer technique**:

1. **Initialize two pointers**: One at the beginning (`i = 0`) and the other at the end (`j = len(height) - 1`).
2. **Compute the area**: The area is calculated as `min(height[i], height[j]) * (j - i)`, where the minimum height determines the water level.
3. **Move the pointers**: To maximize the area, we always move the pointer pointing to the **shorter line**, since moving the taller line won't help increase the height constraint.
4. **Update the maximum area**: Track the maximum area encountered during the iteration.
5. **Repeat until `i` and `j` meet**.

This approach ensures an efficient **O(n) time complexity**, making it optimal for large inputs.

