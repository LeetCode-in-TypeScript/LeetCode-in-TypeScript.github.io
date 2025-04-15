[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 222\. Count Complete Tree Nodes

Medium

Given the `root` of a **complete** binary tree, return the number of the nodes in the tree.

According to **[Wikipedia](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between `1` and <code>2<sup>h</sup></code> nodes inclusive at the last level `h`.

Design an algorithm that runs in less than `O(n)` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)

**Input:** root = [1,2,3,4,5,6]

**Output:** 6 

**Example 2:**

**Input:** root = []

**Output:** 0 

**Example 3:**

**Input:** root = [1]

**Output:** 1 

**Constraints:**

*   The number of nodes in the tree is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.
*   <code>0 <= Node.val <= 5 * 10<sup>4</sup></code>
*   The tree is guaranteed to be **complete**.

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
function countNodes(root: TreeNode | null): number {
    if (root === null) {
        return 0
    }
    const leftHeight = getLeftHeight(root)
    const rightHeight = getRightHeight(root)
    if (leftHeight === rightHeight) {
        return (1 << leftHeight) - 1
    } else {
        return 1 + countNodes(root.left) + countNodes(root.right)
    }
}

function getLeftHeight(node: TreeNode | null): number {
    let height = 0
    while (node !== null) {
        height++
        node = node.left
    }
    return height
}

function getRightHeight(node: TreeNode | null): number {
    let height = 0
    while (node !== null) {
        height++
        node = node.right
    }
    return height
}

export { countNodes }
```