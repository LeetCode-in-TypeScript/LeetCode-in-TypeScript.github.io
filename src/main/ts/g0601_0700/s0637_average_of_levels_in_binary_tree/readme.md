[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 637\. Average of Levels in Binary Tree

Easy

Given the `root` of a binary tree, return _the average value of the nodes on each level in the form of an array_. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/09/avg1-tree.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** [3.00000,14.50000,11.00000] Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/09/avg2-tree.jpg)

**Input:** root = [3,9,20,15,7]

**Output:** [3.00000,14.50000,11.00000]

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.
*   <code>-2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1</code>

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
function averageOfLevels(root: TreeNode | null): number[] {
    if (!root) {
        return []
    }
    let res = []
    let queue = [root]
    while (queue.length) {
        let len = queue.length
        let sum = 0
        for (let i = 0; i < len; i++) {
            let node = queue.shift()
            sum += node.val
            if (node.left) {
                queue.push(node.left)
            }
            if (node.right) {
                queue.push(node.right)
            }
        }
        res.push(sum / len)
    }
    return res
}

export { averageOfLevels }
```