# [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i-th` day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

> **Example 1:**  
> Input: `temperatures = [73,74,75,71,69,72,76,73]`  
> Output: `[1,1,4,2,1,1,0,0]`

> **Example 2:**  
> Input: `temperatures = [30,40,50,60]`  
> Output: `[1,1,1,0]`

> **Example 3:**  
> Input: `temperatures = [30,60,90]`  
> Output: `[1,1,0]`

### Constraints:
- 1 <= temperatures.length <= 10⁵  
- 30 <= temperatures[i] <= 100

---

## My Code

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        ans = [0] * len(temperatures)
        stack = []
        for idx, temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < temp:
                i = stack.pop()
                ans[i] = idx - i
            stack.append(idx)
        return ans
```

---

## Explanation

This solution uses a monotonic decreasing stack to keep track of indices of temperatures that haven't found a warmer day yet. As we iterate through each day's temperature, we check whether it is warmer than the last stored temperature in the stack.

If it is, we pop from the stack and calculate how many days it took to reach this warmer temperature, storing that result in the answer array. We keep doing this until the stack is either empty or the current temperature is not warmer. Finally, if there are no warmer temperatures ahead, the value remains `0` (which we initialized by default).

This approach ensures every temperature is pushed and popped at most once, making it efficient with O(n) time complexity.
