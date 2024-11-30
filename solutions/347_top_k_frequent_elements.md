# [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)
![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order.

### Example 1:
> **Input:** `nums = [1,1,1,2,2,3]`, `k = 2`  
> **Output:** `[1,2]`

### Example 2:
> **Input:** `nums = [1]`, `k = 1`  
> **Output:** `[1]`

### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `k` is in the range `[1, the number of unique elements in the array]`.
- It is guaranteed that the answer is unique.

### Follow up:  
Your algorithm's time complexity must be better than `O(n log n)`, where `n` is the array's size.

## My Code

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        hash_table = defaultdict(int)
        for num in nums:
            hash_table[num] += 1
        hash_table_top_k = sorted(hash_table.items(), key=lambda x: x[1], reverse=True)[:k]
        return [h[0] for h in hash_table_top_k]
```



## Explanation of the Code

This solution aims to find the top `k` most frequent elements in the given array `nums`. Here's how it works:

1. **Counting Frequencies:**  
   A `defaultdict` is used to count the frequency of each element in `nums`. As we iterate through the array, each element's count is incremented in the hash table.

2. **Sorting by Frequency:**  
   The `items()` method is called on the hash table, returning a list of tuples `(element, frequency)`. The `sorted()` function is used to sort this list by frequency in descending order using a lambda function `key=lambda x: x[1]`.

3. **Extracting Top K Elements:**  
   We slice the sorted list to take the first `k` elements and use list comprehension to extract just the elements (not their frequencies), returning the result.

This approach is efficient but can be optimized using a heap to achieve the required time complexity of better than `O(n log n)`.
