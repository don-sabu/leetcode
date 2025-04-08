# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses)

![Static Badge](https://img.shields.io/badge/Difficulty-Easy-brightgreen)

## Problem Statement

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
- Every close bracket has a corresponding open bracket of the same type.

> **Example 1:**  
> Input: s = `"()"`  
> Output: `true`

> **Example 2:**  
> Input: s = `"()[]{}"`  
> Output: `true`

> **Example 3:**  
> Input: s = `"(]"`  
> Output: `false`

> **Example 4:**  
> Input: s = `"([])"`  
> Output: `true`

### Constraints:

- 1 <= `s.length` <= 10⁴  
- `s` consists of parentheses only `'()[]{}'`.

---

## My Code

```python
class Solution:
    def isValid(self, s: str) -> bool:
        opening = ['{', '[', '(']
        closing = ['}', ']', ')']
        brackets = {')': '(', 
                    ']': '[', 
                    '}': '{'}
        stack = []
        for i in s:
            if i in opening:
                stack.append(i)
            else:
                if not stack or brackets[i] != stack.pop():
                    return False
        return not stack
```

---

## Explanation

The solution uses a **stack** to validate the matching and ordering of brackets. Every time an opening bracket is encountered (`(`, `{`, `[`), it’s pushed onto the stack. When a closing bracket is found, the code checks if the top of the stack matches the corresponding opening bracket. If not, or if the stack is empty, the string is invalid.

At the end, if the stack is empty, it means all brackets were properly closed and matched. Otherwise, some opening brackets were not matched, and the string is invalid. This approach ensures **O(n)** time complexity and is optimal for this problem.
