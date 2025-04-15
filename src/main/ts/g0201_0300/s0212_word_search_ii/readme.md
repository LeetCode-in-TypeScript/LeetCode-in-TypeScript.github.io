[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 212\. Word Search II

Hard

Given an `m x n` `board` of characters and a list of strings `words`, return _all words on the board_.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

**Input:** board = \[\["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]

**Output:** ["eat","oath"] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)

**Input:** board = \[\["a","b"],["c","d"]], words = ["abcb"]

**Output:** [] 

**Constraints:**

*   `m == board.length`
*   `n == board[i].length`
*   `1 <= m, n <= 12`
*   `board[i][j]` is a lowercase English letter.
*   <code>1 <= words.length <= 3 * 10<sup>4</sup></code>
*   `1 <= words[i].length <= 10`
*   `words[i]` consists of lowercase English letters.
*   All the strings of `words` are unique.

## Solution

```typescript
class Tree {
    children: Map<string, Tree>
    end: string | null

    constructor() {
        this.children = new Map()
        this.end = null
    }

    static addWord(node: Tree, word: string): void {
        let cur = node
        for (const char of word) {
            if (!cur.children.has(char)) {
                cur.children.set(char, new Tree())
            }
            cur = cur.children.get(char)!
        }
        cur.end = word
    }

    static deleteWord(node: Tree, word: string): void {
        const stack: [Tree, string][] = []
        let cur = node
        for (const char of word) {
            const next = cur.children.get(char)
            if (!next) return
            stack.push([cur, char])
            cur = next
        }
        cur.end = null
        for (let i = stack.length - 1; i >= 0; i--) {
            const [parent, char] = stack[i]
            const child = parent.children.get(char)!
            if (child.children.size === 0 && child.end === null) {
                parent.children.delete(char)
            } else {
                break
            }
        }
    }

    getChild(char: string): Tree | null {
        return this.children.get(char) || null
    }

    len(): number {
        return this.children.size
    }
}

function findWords(board: string[][], words: string[]): string[] {
    if (board.length === 0 || board[0].length === 0) {
        return []
    }
    const root = new Tree()
    for (const word of words) {
        Tree.addWord(root, word)
    }
    const collected: string[] = []
    for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[0].length; j++) {
            dfs(board, i, j, root, collected, root)
        }
    }
    return collected
}

function dfs(board: string[][], i: number, j: number, cur: Tree, collected: string[], root: Tree): void {
    const c = board[i][j]
    if (c === '-') {
        return
    }
    const next = cur.getChild(c)
    if (!next) {
        return
    }
    if (next.end !== null) {
        collected.push(next.end)
        const word = next.end
        next.end = null
        if (next.len() === 0) {
            Tree.deleteWord(root, word)
        }
    }
    board[i][j] = '-'
    if (i > 0) {
        dfs(board, i - 1, j, next, collected, root)
    }
    if (i + 1 < board.length) {
        dfs(board, i + 1, j, next, collected, root)
    }
    if (j > 0) {
        dfs(board, i, j - 1, next, collected, root)
    }
    if (j + 1 < board[0].length) {
        dfs(board, i, j + 1, next, collected, root)
    }
    board[i][j] = c
}

export { findWords }
```