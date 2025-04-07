[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 103\. Binary Tree Zigzag Level Order Traversal

Medium

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** [[3],[20,9],[15,7]] 

**Example 2:**

**Input:** root = [1]

**Output:** [[1]] 

**Example 3:**

**Input:** root = []

**Output:** [] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-100 <= Node.val <= 100`

## Solution

```typescript
import { TreeNode } from '../../com_github_leetcode/treenode'

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */
function zigzagLevelOrder(root: TreeNode | null): number[][] {
    const result: number[][] = []
    if (root === null) {
        return result
    }
    const q: (TreeNode | null)[] = [root, null]
    let zig = true
    let level: number[] = []
    while (q.length > 0) {
        const node = q.shift()
        if (node === null) {
            result.push(level)
            zig = !zig
            level = []
            if (q.length > 0) {
                q.push(null)
            }
        } else {
            if (zig) {
                level.push(node.val)
            } else {
                level.unshift(node.val)
            }
            if (node.left !== null) {
                q.push(node.left)
            }
            if (node.right !== null) {
                q.push(node.right)
            }
        }
    }
    return result
}

export { zigzagLevelOrder }
```