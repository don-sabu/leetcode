# [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

> **Example 1:**
> 
> Input: s = `"A man, a plan, a canal: Panama"`  
> Output: `true`  
> Explanation: `"amanaplanacanalpanama"` is a palindrome.

> **Example 2:**
> 
> Input: s = `"race a car"`  
> Output: `false`  
> Explanation: `"raceacar"` is not a palindrome.

> **Example 3:**
> 
> Input: s = `" "`  
> Output: `true`  
> Explanation: `s` is an empty string `""` after removing non-alphanumeric characters.  
> Since an empty string reads the same forward and backward, it is a palindrome.

### Constraints:

- 1 <= `s.length` <= 2 * 10⁵  
- `s` consists only of printable ASCII characters.  

## My Code
```c
bool isPalindrome(char* s) {
    int len = strlen(s);
    int i = 0, j = len - 1;
    
    while (i < j) {
        while (i < j && !isalnum(s[i]))
            i++;
        while (i < j && !isalnum(s[j]))
            j--;
        if (tolower(s[i]) != tolower(s[j]))
            return false;
        i++;
        j--;
    }
    return true;
}
```

## Explanation

This solution uses the **two-pointer technique** to efficiently check if the given string is a palindrome.

1. It initializes two pointers: `i` at the beginning and `j` at the end of the string.
2. It skips all non-alphanumeric characters by advancing `i` and `j` accordingly.
3. It compares characters at `i` and `j`, ignoring case differences.
4. If any pair of characters don’t match, the function returns `false`.
5. If all character pairs match, the function returns `true`.

This approach runs in **O(n) time complexity**, where `n` is the length of the string, as each character is processed at most once.
