# [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in `O(n)` time.

> **Example 1:**
>
> Input: nums = [100,4,200,1,3,2]  
> Output: 4  
> Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.  
>
> **Example 2:**
>
> Input: nums = [0,3,7,2,5,8,4,6,0,1]  
> Output: 9  
>
> **Example 3:**
>
> Input: nums = [1,0,1,2]  
> Output: 3  

### Constraints:
- `0 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

## My Code

```python
from typing import List

class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums = set(nums)
        max_seq = 0

        for n in nums:
            if n-1 not in nums and n + max_seq in nums:
                seq = 1
                cur = n
                while cur + 1 in nums:
                    seq += 1
                    cur += 1
                max_seq = max(max_seq, seq)

        return max_seq
```

## Explanation

The problem requires finding the longest consecutive sequence in an unsorted array in `O(n)` time complexity. The approach used in the solution:

1. **Convert the array into a set**: This allows `O(1)` lookup time when checking for consecutive elements.
2. **Iterate through each number**: We only start counting a sequence if the current number is the start of a sequence (i.e., `n-1` is not in the set).
3. **Expand the sequence**: Once a sequence is found, we continue checking the next numbers in order until the sequence ends.
4. **Keep track of the longest sequence**: We update `max_seq` whenever a longer sequence is found.

This ensures an efficient approach with a time complexity of `O(n)`, as each number is processed only once.

