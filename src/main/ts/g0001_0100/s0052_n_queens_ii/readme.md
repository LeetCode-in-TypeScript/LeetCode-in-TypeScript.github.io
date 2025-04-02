[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 52\. N-Queens II

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _the number of distinct solutions to the **n-queens puzzle**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** 2

**Explanation:** There are two distinct solutions to the 4-queens puzzle as shown. 

**Example 2:**

**Input:** n = 1

**Output:** 1 

**Constraints:**

*   `1 <= n <= 9`

## Solution

```typescript
function totalNQueens(n: number): number {
    function solve(r: number, cols: boolean[], diag: boolean[], antiDiag: boolean[]): number {
        if (r === n) {
            return 1
        }
        let count = 0
        for (let c = 0; c < n; c++) {
            if (!cols[c] && !diag[r + c] && !antiDiag[r - c + n - 1]) {
                cols[c] = diag[r + c] = antiDiag[r - c + n - 1] = true
                count += solve(r + 1, cols, diag, antiDiag)
                cols[c] = diag[r + c] = antiDiag[r - c + n - 1] = false
            }
        }
        return count
    }
    return solve(0, new Array(n).fill(false), new Array(2 * n - 1).fill(false), new Array(2 * n - 1).fill(false))
}

export { totalNQueens }
```