# [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram)

![Static Badge](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem Statement

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

> **Example 1:**  
> Input: `heights = [2,1,5,6,2,3]`  
> Output: `10`  
> Explanation: The histogram looks like this:
> ```
> 6      █
> 5      █ █
> 4      █ █
> 3      █ █   █
> 2  █   █ █ █ █
> 1  █ █ █ █ █ █
>    0 1 2 3 4 5
> ```
> The largest rectangle has area 10 (bars at index 2 and 3 with height 5 and 6).

> **Example 2:**  
> Input: `heights = [2,4]`  
> Output: `4`  
> Explanation: The histogram looks like:
> ```
> 4     █
> 3     █
> 2  █  █
> 1  █  █
>    0  1
> ```
> The largest rectangle has area 4.

### Constraints:
- `1 <= heights.length <= 10⁵`
- `0 <= heights[i] <= 10⁴`

---

## My Code

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []
        max_area = 0
        for idx, h in enumerate(heights):
            if not stack:
                stack.append((idx, h))
                max_area = h
            else:
                if stack[-1][1] > h:
                    while stack and stack[-1][1] > h:
                        i, low_h = stack.pop()
                        max_area = max(max_area, (idx - i) * low_h)
                    stack.append((i, h))
                else:
                    stack.append((idx, h))
        while stack:
            i, low_h = stack.pop()
            max_area = max(max_area, (len(heights) - i) * low_h)
        return max_area
```

---

## Explanation

This solution uses a **monotonic increasing stack** to keep track of the indices and heights of bars. The idea is to process each bar and compute potential largest areas when a shorter bar is found. When the current bar is smaller than the top of the stack, we pop from the stack and calculate the area considering that popped bar as the smallest in the rectangle.

We continue this process while the current bar is smaller than the top of the stack. Finally, after the main loop, any bars remaining in the stack are processed assuming they extend till the end of the histogram.

This approach ensures each bar is pushed and popped at most once, making it efficient with a time complexity of **O(n)**.
