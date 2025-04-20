[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 54\. Spiral Matrix

Medium

Given an `m x n` `matrix`, return _all elements of the_ `matrix` _in spiral order_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

**Input:** matrix = \[\[1,2,3],[4,5,6],[7,8,9]]

**Output:** [1,2,3,6,9,8,7,4,5] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

**Input:** matrix = \[\[1,2,3,4],[5,6,7,8],[9,10,11,12]]

**Output:** [1,2,3,4,8,12,11,10,9,5,6,7] 

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 10`
*   `-100 <= matrix[i][j] <= 100`

## Solution

```typescript
function spiralOrder(matrix: number[][]): number[] {
    const result: number[] = []
    let r = 0,
        c = 0
    let bigR = matrix.length - 1
    let bigC = matrix[0].length - 1
    while (r <= bigR && c <= bigC) {
        for (let i = c; i <= bigC; i++) {
            result.push(matrix[r][i])
        }
        r++
        for (let i = r; i <= bigR; i++) {
            result.push(matrix[i][bigC])
        }
        bigC--
        for (let i = bigC; i >= c && r <= bigR; i--) {
            result.push(matrix[bigR][i])
        }
        bigR--
        for (let i = bigR; i >= r && c <= bigC; i--) {
            result.push(matrix[i][c])
        }
        c++
    }
    return result
}

export { spiralOrder }
```