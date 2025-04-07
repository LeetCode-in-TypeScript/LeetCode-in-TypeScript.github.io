[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 77\. Combinations

Medium

Given two integers `n` and `k`, return _all possible combinations of_ `k` _numbers out of the range_ `[1, n]`.

You may return the answer in **any order**.

**Example 1:**

**Input:** n = 4, k = 2

**Output:** [ [2,4], [3,4], [2,3], [1,2], [1,3], [1,4], ] 

**Example 2:**

**Input:** n = 1, k = 1

**Output:** [[1]] 

**Constraints:**

*   `1 <= n <= 20`
*   `1 <= k <= n`

## Solution

```typescript
function combine(n: number, k: number): number[][] {
    const ans: number[][] = []
    const backtrack = (curr: number[], j: number) => {
        if (curr.length == k) {
            ans.push([...curr])
            return
        }
        for (let i = j; i <= n; i++) {
            curr.push(i)
            backtrack(curr, i + 1)
            curr.pop()
        }
    }
    backtrack([], 1)
    return ans
}

export { combine }
```