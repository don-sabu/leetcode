# [1. Two Sum](https://leetcode.com/problems/two-sum)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:
> **Input:** nums = [2,7,11,15], target = 9  
> **Output:** [0,1]  
> **Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

### Example 2:
> **Input:** nums = [3,2,4], target = 6  
> **Output:** [1,2]

### Example 3:
> **Input:** nums = [3,3], target = 6  
> **Output:** [0,1]  

### Constraints:
- 2 <= nums.length <= 10<sup>4</sup>
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>
- -10<sup>9</sup> <= target <= 10<sup>9</sup>
- Only one valid answer exists.

---

## My Code

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        n = len(nums)
        hashmap = {}
        for i in range(n):
            complement = target - nums[i]
            if complement in hashmap:
                return [hashmap[complement], i]
            hashmap[nums[i]] = i
```


## Explanation

The solution uses a **hash map** (dictionary) to efficiently track numbers we’ve seen and their indices while iterating through the list. This allows us to check for the required complement in constant time.

### Step-by-Step Breakdown:
1. **Initialize a Hash Map:** We create an empty hash map `hashmap` to store numbers and their corresponding indices as we iterate.
   
2. **Calculate the Complement:** For each number `nums[i]`, we compute the complement by subtracting the current number from the target:  
   `complement = target - nums[i]`.

3. **Check if Complement Exists:**  
   - If the `complement` is already in the hash map, we’ve found the two numbers that sum to the target, so we return their indices:  
     `return [hashmap[complement], i]`.
   - If not, we add the current number and its index to the hash map:  
     `hashmap[nums[i]] = i`.

4. **Efficiency:**  
   - Each lookup and insertion into the hash map is **O(1)**, making the overall time complexity **O(n)**, where `n` is the length of the input list.
   - The space complexity is also **O(n)** because of the additional space used by the hash map.

### Example Walkthrough:
For `nums = [2, 7, 11, 15]` and `target = 9`:
- `i = 0`: `nums[0] = 2`, complement = `9 - 2 = 7` (not in hashmap, add `{2: 0}`).
- `i = 1`: `nums[1] = 7`, complement = `9 - 7 = 2` (found in hashmap).  
  Return `[0, 1]`.

This efficient approach ensures that we find the solution in a single pass through the array.
