# [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

You are given an array of strings `tokens` that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

**Note that:**

- The valid operators are '+', '-', '*', and '/'.
- Each operand may be an integer or another expression.
- The division between two integers always truncates toward zero.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a 32-bit integer.

> **Example 1:**  
> Input: `tokens = ["2","1","+","3","*"]`  
> Output: `9`  
> Explanation: ((2 + 1) * 3) = 9  

> **Example 2:**  
> Input: `tokens = ["4","13","5","/","+"]`  
> Output: `6`  
> Explanation: (4 + (13 / 5)) = 6  

> **Example 3:**  
> Input: `tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]`  
> Output: `22`  
> Explanation:  
> ((10 * (6 / ((9 + 3) * -11))) + 17) + 5  
> = ((10 * (6 / (12 * -11))) + 17) + 5  
> = ((10 * (6 / -132)) + 17) + 5  
> = ((10 * 0) + 17) + 5  
> = (0 + 17) + 5  
> = 17 + 5 = 22  

### Constraints:

- 1 <= tokens.length <= 10⁴  
- `tokens[i]` is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

---

## My Code

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for t in tokens:
            if t in '+-*/':
                b = stack.pop()
                a = stack.pop()
                if t == '+':
                    stack.append(a + b)
                elif t == '-':
                    stack.append(a - b)
                elif t == '*':
                    stack.append(a * b)
                elif t == '/':
                    stack.append(int(a / b))
            else:
                stack.append(int(t))
        return stack.pop()
```

---

## Explanation

This solution uses a stack to evaluate the expression in reverse Polish notation. We iterate through each token: if the token is a number, we simply push it onto the stack. If it's an operator, we pop the top two numbers from the stack, apply the operation, and push the result back.

Division is handled using `int(a / b)` to ensure truncation towards zero, as required. Once all tokens are processed, the last item on the stack is the final result. This approach ensures efficient and clean evaluation of the RPN expression in linear time.

We can use isdigit(). But this approach is faster.