# [155. Min Stack](https://leetcode.com/problems/min-stack/)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element val onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with O(1) time complexity for each function.

> **Example 1:**  
> Input  
> `["MinStack","push","push","push","getMin","pop","top","getMin"]`  
> `[[],[-2],[0],[-3],[],[],[],[]]`  
> Output  
> `[null,null,null,null,-3,null,0,-2]`  
>  
> Explanation  
> `MinStack minStack = new MinStack();`  
> `minStack.push(-2);`  
> `minStack.push(0);`  
> `minStack.push(-3);`  
> `minStack.getMin(); // return -3`  
> `minStack.pop();`  
> `minStack.top();    // return 0`  
> `minStack.getMin(); // return -2`

### Constraints:

- -2³¹ <= val <= 2³¹ - 1  
- Methods `pop`, `top`, and `getMin` operations will always be called on non-empty stacks.  
- At most 3 × 10⁴ calls will be made to `push`, `pop`, `top`, and `getMin`.

---

## My Code

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = []
        
    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack:
            self.min_stack.append(val)
        else:
            self.min_stack.append(min(self.min_stack[-1], val))

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```
## Explanation

The first solution uses two stacks—one for storing values and another (`min_stack`) for keeping track of the current minimum at each level of the main stack. This ensures that both `push` and `getMin` work in constant time.

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.minimum = float('inf')
        
    def push(self, val: int) -> None:
        if not self.stack:
            self.stack.append(val)
            self.minimum = val
        else:
            if val < self.minimum:
                self.stack.append(2 * val - self.minimum)
                self.minimum = val
            else:
                self.stack.append(val)

    def pop(self) -> None:
        top = self.stack.pop()
        if top < self.minimum:
            self.minimum = 2 * self.minimum - top

    def top(self) -> int:
        if not self.stack:
            return

        top = self.stack[-1]
        if top < self.minimum:
            return self.minimum
        else:
            return top

    def getMin(self) -> int:
        return self.minimum
```

---

## Explanation

The second approach is more space-efficient and uses mathematical encoding. When a value smaller than the current minimum is pushed, it's encoded with a transformation (`2*val - min`) so that when we pop and decode it, we can restore the previous minimum. This clever trick also keeps `getMin()` and `push()` in constant time and uses just one stack.
