[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 69\. Sqrt(x)

Easy

Given a non-negative integer `x`, compute and return _the square root of_ `x`.

Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

**Note:** You are not allowed to use any built-in exponent function or operator, such as `pow(x, 0.5)` or `x ** 0.5`.

**Example 1:**

**Input:** x = 4

**Output:** 2 

**Example 2:**

**Input:** x = 8

**Output:** 2

**Explanation:** The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.

**Constraints:**

*   <code>0 <= x <= 2<sup>31</sup> - 1</code>

## Solution

```typescript
function mySqrt(x: number): number {
    let low = 1
    let high = x
    let lowest = 0
    while (low <= high) {
        const mid = Math.floor((low + high) / 2)
        const pow = mid * mid
        if (pow > x) {
            high = mid - 1
        } else if (pow < x) {
            low = mid + 1
            lowest = mid
        } else {
            return mid
        }
    }
    return lowest
}

export { mySqrt }
```