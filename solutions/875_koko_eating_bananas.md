# [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Koko loves to eat bananas. There are `n` piles of bananas, the `i-th` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the **minimum integer `k`** such that she can eat all the bananas within `h` hours.

> **Example 1:**  
> Input: `piles = [3,6,7,11], h = 8`  
> Output: `4`

> **Example 2:**  
> Input: `piles = [30,11,23,4,20], h = 5`  
> Output: `30`

> **Example 3:**  
> Input: `piles = [30,11,23,4,20], h = 6`  
> Output: `23`

### Constraints:
- `1 <= piles.length <= 10⁴`
- `piles.length <= h <= 10⁹`
- `1 <= piles[i] <= 10⁹`

---

## My Code

### First solution:
```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        left = 1
        right = max(piles)

        while left <= right:
            mid = (left + right) // 2
            k = sum((pile + mid - 1) // mid for pile in piles)
            if k > h:
                left = mid + 1
            else:
                right = mid - 1
        return left
```

### Optimized version:
```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        left = -(-sum(piles) // h)
        right = max(piles)
        time = lambda n: sum(-(-pile // n) for pile in piles)

        if time(left) <= h:
            return left

        while left < right:
            mid = (left + right) // 2
            if time(mid) > h:
                left = mid + 1
            else:
                right = mid
        return left
```

---

## Explanation

The problem requires finding the minimum eating speed (`k`) such that Koko finishes all bananas within `h` hours. This is a classic optimization problem that can be solved efficiently with **binary search**.

In both solutions, we search between a lower bound (`1` or a more optimized value like `ceil(sum(piles)/h)`) and the upper bound (`max(piles)`), checking if Koko can finish all piles at a given speed (`mid`). For each speed, we calculate the total hours required to eat all the bananas using ceiling division. If it takes more than `h` hours, we increase the speed; otherwise, we try a slower speed to minimize `k`.

The optimized solution improves the lower bound to reduce the number of iterations and uses concise logic with a lambda function to compute time, making it more efficient overall.

---

### Why use `(pile + mid - 1) // mid` and `-(-x // y)` instead of `ceil(x / y)`?

In both solutions, we aim to avoid using the `math.ceil()` function because it is **slightly slower** and requires an import. Instead, we use **clever integer arithmetic tricks** that achieve the same result more efficiently.

#### 1. `(pile + mid - 1) // mid` is equivalent to `ceil(pile / mid)`

This formula ensures that any remainder results in rounding up. For example:

* `pile = 10`, `mid = 3`
* `10 / 3 = 3.33`, `ceil(10 / 3) = 4`
* `(10 + 3 - 1) // 3 = 12 // 3 = 4` ✅

This method is **faster**, avoids floating-point arithmetic, and does not require importing the `math` module.

#### 2. `-(-x // y)` is also equivalent to `ceil(x / y)`

This trick works because:

* The regular `x // y` does **floor division**
* Negating `x`, performing floor division, and negating the result again effectively gives the **ceiling of x / y**

Example:

* `x = 10`, `y = 3`
* `10 / 3 = 3.33`, `ceil(10 / 3) = 4`
* `-(-10 // 3) = -(-4) = 4` ✅

This trick is especially handy for initializing bounds like `left = ceil(sum(piles) / h)` in binary search, but faster and cleaner.
