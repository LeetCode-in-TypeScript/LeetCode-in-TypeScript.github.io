[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 63\. Unique Paths II

Medium

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and space is marked as `1` and `0` respectively in the grid.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

**Input:** obstacleGrid = \[\[0,0,0],[0,1,0],[0,0,0]]

**Output:** 2

**Explanation:** There is one obstacle in the middle of the 3x3 grid above. There are two ways to reach the bottom-right corner: 1. Right -> Right -> Down -> Down 2. Down -> Down -> Right -> Right 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

**Input:** obstacleGrid = \[\[0,1],[0,0]]

**Output:** 1 

**Constraints:**

*   `m == obstacleGrid.length`
*   `n == obstacleGrid[i].length`
*   `1 <= m, n <= 100`
*   `obstacleGrid[i][j]` is `0` or `1`.

## Solution

```typescript
function uniquePathsWithObstacles(obstacleGrid: number[][]): number {
    if (obstacleGrid[0][0] === 1) {
        return 0
    }
    obstacleGrid[0][0] = 1
    const m = obstacleGrid.length
    const n = obstacleGrid[0].length
    for (let i = 1; i < m; i++) {
        if (obstacleGrid[i][0] === 1) {
            obstacleGrid[i][0] = 0
        } else {
            obstacleGrid[i][0] = obstacleGrid[i - 1][0]
        }
    }
    for (let j = 1; j < n; j++) {
        if (obstacleGrid[0][j] === 1) {
            obstacleGrid[0][j] = 0
        } else {
            obstacleGrid[0][j] = obstacleGrid[0][j - 1]
        }
    }
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (obstacleGrid[i][j] === 1) {
                obstacleGrid[i][j] = 0
            } else {
                obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1]
            }
        }
    }
    return obstacleGrid[m - 1][n - 1]
}

export { uniquePathsWithObstacles }
```