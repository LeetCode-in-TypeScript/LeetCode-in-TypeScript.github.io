[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 100\. Same Tree

Easy

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

**Input:** p = [1,2,3], q = [1,2,3]

**Output:** true 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

**Input:** p = [1,2], q = [1,null,2]

**Output:** false 

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

**Input:** p = [1,2,1], q = [1,1,2]

**Output:** false 

**Constraints:**

*   The number of nodes in both trees is in the range `[0, 100]`.
*   <code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code>

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
function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    if (p === null || q === null) {
        return p === null && q === null
    }
    const b1 = isSameTree(p.left, q.left)
    const b2 = isSameTree(p.right, q.right)
    return p.val === q.val && b1 && b2
}

export { isSameTree }
```