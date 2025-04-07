[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 120\. Triangle

Medium

Given a `triangle` array, return _the minimum path sum from top to bottom_.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

**Input:** triangle = \[\[2],[3,4],[6,5,7],[4,1,8,3]]

**Output:** 11

**Explanation:**

    The triangle looks like:
        2
       3 4
      6 5 7
     4 1 8 3
     The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above). 

**Example 2:**

**Input:** triangle = \[\[-10]]

**Output:** -10 

**Constraints:**

*   `1 <= triangle.length <= 200`
*   `triangle[0].length == 1`
*   `triangle[i].length == triangle[i - 1].length + 1`
*   <code>-10<sup>4</sup> <= triangle[i][j] <= 10<sup>4</sup></code>

**Follow up:** Could you do this using only `O(n)` extra space, where `n` is the total number of rows in the triangle?

## Solution

```typescript
function minimumTotal(triangle: number[][]): number {
    if (!triangle || triangle.length === 0) {
        return 0
    }
    const rows = triangle.length
    const cols = triangle[rows - 1].length
    const dp: number[][] = Array.from({ length: rows }, () => Array(cols).fill(-10001))
    function dfs(row: number, col: number): number {
        if (row >= triangle.length) {
            return 0
        }
        if (dp[row][col] !== -10001) {
            return dp[row][col]
        }
        const sum = triangle[row][col] + Math.min(dfs(row + 1, col), dfs(row + 1, col + 1))
        dp[row][col] = sum
        return sum
    }
    return dfs(0, 0)
}

export { minimumTotal }
```