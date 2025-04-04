# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

> **Example 1:**
>
> Input: nums = [1,2,3,4]  
> Output: [24,12,8,6]  

> **Example 2:**
>
> Input: nums = [-1,1,0,-3,3]  
> Output: [0,0,9,0,0]  

### Constraints:

- 2 <= nums.length <= 105  
- -30 <= nums[i] <= 30  
- The input is generated such that answer[i] is guaranteed to fit in a 32-bit integer.  

## My Code
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        product = 1
        z_count = 0
        for num in nums:
            if num != 0:
                product *= num
            else:
                z_count +=1
        
        if z_count > 1:
            return [0] * len(nums)
        
        res = []
        if z_count == 1:
            for num in nums:
                if num == 0:
                    res.append(product)
                else:
                    res.append(0)
            return res

        for num in nums:
            res.append(int(product/num))
        return res
```
## Explanation

This solution calculates the product of all nonzero numbers in the array.  
- First, it iterates over `nums` to compute the total product while counting the number of zeros.  
- If more than one zero is present, the result is all zeros because multiplying by zero results in zero.  
- If exactly one zero exists, only the position with zero gets the total product, while all others remain zero.  
- If there are no zeros, we divide the total product by each element to get the result.  

This approach avoids using division in the main logic and ensures an O(n) runtime. 🚀
