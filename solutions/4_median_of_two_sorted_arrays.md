# [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays)
![Static Badge](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem Statement

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m + n)).

### Example 1:
Input: `nums1 = [1,3]`, `nums2 = [2]`
Output: `2.00000`
Explanation: merged array = [1,2,3] and median is 2.

### Example 2:
Input: `nums1 = [1,2]`, `nums2 = [3,4]`
Output: `2.50000`
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

### Constraints:
- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-10^6 <= nums1[i], nums2[i] <= 10^6`

## My Code

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        int p1 = 0, p2 = 0;
        int mid1 = 0, mid2 = 0;
        
        for(int i = 0; i <= (m + n) / 2; i++)
        {
            mid1 = mid2;
            if(p1 < m && p2 < n)
            {
                if(nums1[p1] < nums2[p2])
                    mid2 = nums1[p1++];
                else
                    mid2 = nums2[p2++];
            }
            else if(p1 < m)
            {
                mid2 = nums1[p1++];
            }
            else
            {
                mid2 = nums2[p2++];
            }
        }
        
        if((m + n) % 2 == 0)
            return (double)(mid1 + mid2) / 2;
        else
            return mid2;
    }
}
```



## Explanation of the Code

In this solution, we aim to find the median of two sorted arrays, `nums1` and `nums2`, without fully merging them. The idea is to traverse both arrays while maintaining two pointers (`p1` and `p2`) that will point to the current elements being compared. We iterate until we reach the middle of the merged arrays.

- The variables `mid1` and `mid2` store the last two elements seen while traversing the arrays.
- At each step of the loop, we compare the current elements of `nums1` and `nums2`. The smaller element gets assigned to `mid2` and the corresponding pointer (`p1` or `p2`) is incremented.
- After the loop, if the total length of the merged array is odd, `mid2` will be the median. If the length is even, the median is the average of `mid1` and `mid2`.

This solution efficiently calculates the median in O(m + n) time complexity, though it doesn't fully merge the arrays, just tracking the necessary elements.
