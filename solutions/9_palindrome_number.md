# [9. Palindrome Number](https://leetcode.com/problems/palindrome-number)
![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement:

Given an integer `x`, return true if `x` is a palindrome, and false otherwise.

> **Example 1:**
>
> Input: `x = 121`
> Output: `true`
> Explanation: 121 reads as 121 from left to right and from right to left.

> **Example 2:**
>
> Input: `x = -121`
> Output: `false`
> Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

> **Example 3:**
>
> Input: `x = 10`
> Output: `false`
> Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

### Constraints:

- $-2^{31} \leq x \leq 2^{31} - 1$

### Follow-up:
Could you solve it without converting the integer to a string?

## Solution Code:

```cpp
bool isPalindrome(int x){
    int r = 0;
    if(x < 0 || (x != 0 && x % 10 == 0))
        return false;
    while(r < x)
    {
        r = r * 10 + x % 10;
        x /= 10;
    }
    return x == r || x == r/10;
}
```

### Explanation:

The code aims to determine if a given integer `x` is a palindrome by comparing it with its reverse.

- **Initial Checks**:
    - If `x` is negative, it cannot be a palindrome, so we return `false`.
    - If `x` is a non-negative number and ends with zero (but is not zero itself), it cannot be a palindrome. This is because a valid palindrome cannot end with zero unless the number is zero.

- **Reversing the Integer**:
    - The integer `x` is gradually reversed in the `while` loop. In each iteration, the last digit of `x` is added to `r` (the reversed number).
    - After each addition, the original number `x` is reduced by removing its last digit (`x /= 10`).

- **Comparison**:
    - Once the reversed number `r` is greater than or equal to `x`, the loop stops.
    - To check if the number is a palindrome, we compare the original `x` with the reversed number `r`.
    - For numbers with an odd number of digits, `r / 10` will remove the last digit of the reversed number, so the comparison becomes `x == r / 10`.

- **Time Complexity**:
    - The time complexity of this approach is O(log(x)) because we are dividing the number by 10 in each iteration, which reduces the number of digits by 1 in each step.

This approach avoids converting the number to a string and works directly with the integer.
