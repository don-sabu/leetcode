# [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

> **Example 1:**  
> Input: `n = 3`  
> Output: `["((()))","(()())","(())()","()(())","()()()"]`  

> **Example 2:**  
> Input: `n = 1`  
> Output: `["()"]`  

### Constraints:
- 1 <= n <= 8

---

## My Code

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        def recursion(o, c, p):
            if o > n or c > n or c > o:
                return
            if o == n and c == n:
                paranthesis.append(p)
                return
            recursion(o+1, c, p+'(')
            recursion(o, c+1, p+')')
        
        paranthesis = []
        recursion(0, 0, '')
        return paranthesis
```

---

## Explanation

The solution uses a recursive backtracking approach. The idea is to build the valid combinations step by step by adding either an opening or closing parenthesis at each stage, ensuring the combination remains valid.

- We maintain two counters: one for the number of opening brackets used (`o`) and one for closing brackets (`c`).
- A combination is valid only if:
  - We don’t use more than `n` open or close parentheses.
  - At no point do we have more closing parentheses than opening ones (i.e., `c <= o`).
- Once we’ve used exactly `n` open and `n` close parentheses, we know we’ve formed a valid expression and add it to the result list.

This technique ensures all valid combinations are generated without exploring invalid paths.
