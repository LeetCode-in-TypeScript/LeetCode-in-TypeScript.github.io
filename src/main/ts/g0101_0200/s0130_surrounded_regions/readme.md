[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 130\. Surrounded Regions

Medium

Given an `m x n` matrix `board` containing `'X'` and `'O'`, _capture all regions that are 4-directionally surrounded by_ `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

**Input:** board = \[\["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]

**Output:** [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]

**Explanation:** Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically. 

**Example 2:**

**Input:** board = \[\["X"]]

**Output:** [["X"]] 

**Constraints:**

*   `m == board.length`
*   `n == board[i].length`
*   `1 <= m, n <= 200`
*   `board[i][j]` is `'X'` or `'O'`.

## Solution

```typescript
/**
 Do not return anything, modify board in-place instead.
 */
function solve(board: string[][]): void {
    if (board.length === 0) {
        return
    }
    const rows = board.length
    const cols = board[0].length
    const dfs = (board: string[][], row: number, col: number): void => {
        if (row < 0 || row >= rows || col < 0 || col >= cols || board[row][col] !== 'O') {
            return
        }
        board[row][col] = '#'
        dfs(board, row + 1, col)
        dfs(board, row - 1, col)
        dfs(board, row, col + 1)
        dfs(board, row, col - 1)
    }
    for (let i = 0; i < cols; i++) {
        if (board[0][i] === 'O') {
            dfs(board, 0, i)
        }
        if (board[rows - 1][i] === 'O') {
            dfs(board, rows - 1, i)
        }
    }
    for (let i = 0; i < rows; i++) {
        if (board[i][0] === 'O') {
            dfs(board, i, 0)
        }
        if (board[i][cols - 1] === 'O') {
            dfs(board, i, cols - 1)
        }
    }
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (board[i][j] === 'O') {
                board[i][j] = 'X'
            }
            if (board[i][j] === '#') {
                board[i][j] = 'O'
            }
        }
    }
}

export { solve }
```