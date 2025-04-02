[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 50\. Pow(x, n)

Medium

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., <code>x<sup>n</sup></code>).

**Example 1:**

**Input:** x = 2.00000, n = 10

**Output:** 1024.00000 

**Example 2:**

**Input:** x = 2.10000, n = 3

**Output:** 9.26100 

**Example 3:**

**Input:** x = 2.00000, n = -2

**Output:** 0.25000

**Explanation:** 2<sup>\-2</sup> = 1/2<sup>2</sup> = 1/4 = 0.25 

**Constraints:**

*   `-100.0 < x < 100.0`
*   <code>-2<sup>31</sup> <= n <= 2<sup>31</sup>-1</code>
*   <code>-10<sup>4</sup> <= x<sup>n</sup> <= 10<sup>4</sup></code>

## Solution

```typescript
function myPow(x: number, n: number): number {
    let nn = BigInt(n)
    let res = 1.0
    if (n < 0) {
        nn = -nn
    }
    while (nn > 0) {
        if (nn % 2n === 1n) {
            nn--
            res *= x
        } else {
            x *= x
            nn /= 2n
        }
    }
    return n < 0 ? 1.0 / res : res
}

export { myPow }
```