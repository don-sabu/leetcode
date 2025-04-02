# [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)

![Static Badge](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem Statement

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

### Example 1:

> **Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]  
> **Output:** 6  
> **Explanation:** The above elevation map (black section) is represented by array `[0,1,0,2,1,0,1,3,2,1,2,1]`. In this case, 6 units of rain water (blue section) are being trapped.

### Example 2:

> **Input:** height = [4,2,0,3,2,5]  
> **Output:** 9  

### Constraints:

- `n == height.length`
- `1 <= n <= 2 * 10^4`
- `0 <= height[i] <= 10^5`

---

## Solution 1: Dynamic Programming

```python
from typing import List

class Solution:
    def trap(self, height: List[int]) -> int:
        l = len(height)
        max_l = [height[0]] * l
        for i in range(1, l):
            max_l[i] = max(max_l[i-1], height[i])
        max_r = [height[l-1]] * l
        for i in range(l-2, -1, -1):
            max_r[i] = max(max_r[i+1], height[i])
        res = 0
        for i in range(l):
            res += min(max_l[i], max_r[i]) - height[i]
        return res
```

---

## Solution 2: Two Pointers Approach

```python
from typing import List

class Solution:
    def trap(self, height: List[int]) -> int:
        l = len(height)
        i = 0
        j = l - 1
        l_max = height[i]
        r_max = height[j]
        res = 0
        while i < j:
            if l_max > height[i]:
                res += l_max - height[i]
            else:
                l_max = height[i]

            if r_max > height[j]:
                res += r_max - height[j]
            else:
                r_max = height[j]
            
            if l_max < r_max:
                i += 1
            else:
                j -= 1
        return res
```

---

## Explanation

### **Solution 1: Dynamic Programming**

This solution uses **precomputed arrays** to store the left and right maximum heights for each index. The key observation is that the amount of trapped water at any position depends on the smallest height of the tallest barrier on either side.

1. **Precompute `max_l` (left max heights)**: We iterate from left to right, keeping track of the highest bar seen so far.
2. **Precompute `max_r` (right max heights)**: We iterate from right to left, keeping track of the highest bar seen so far.
3. **Calculate trapped water**: For each position, the trapped water is given by:
   
   
   
   
   
   `trapped_water = min(max_l[i], max_r[i]) - height[i]`
   
   If the height at that position is already equal to `min(max_l, max_r)`, no water can be trapped.
4. **Time Complexity**: **O(n)** since we traverse the array three times.
5. **Space Complexity**: **O(n)** due to the extra storage of `max_l` and `max_r`.

---

### **Solution 2: Two Pointers Approach**

This is an **optimized solution** using two pointers that reduces space complexity to **O(1)**.

1. **Initialize two pointers**: `i` at the leftmost index and `j` at the rightmost index.
2. **Track left and right max heights dynamically**:
   - `l_max` stores the max height encountered so far from the left.
   - `r_max` stores the max height encountered so far from the right.
3. **Move pointers inward**:
   - If `l_max < r_max`, move the left pointer `i` to the right and update `l_max`.
   - Otherwise, move the right pointer `j` to the left and update `r_max`.
4. **Accumulate trapped water**: If the current height at `i` or `j` is less than `l_max` or `r_max`, respectively, water is trapped, and we add the difference to the result.
5. **Time Complexity**: **O(n)** since we traverse the array once.
6. **Space Complexity**: **O(1)** since we only use a few extra variables.

This approach is **more efficient** in terms of space while maintaining the same time complexity as the first solution.

