[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 129\. Sum Root to Leaf Numbers

Medium

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

*   For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.

Return _the total sum of all root-to-leaf numbers_. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

**Input:** root = [1,2,3]

**Output:** 25

**Explanation:** The root-to-leaf path `1->2` represents the number `12`. The root-to-leaf path `1->3` represents the number `13`. Therefore, sum = 12 + 13 = `25`. 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg)

**Input:** root = [4,9,0,5,1]

**Output:** 1026

**Explanation:** The root-to-leaf path `4->9->5` represents the number 495. The root-to-leaf path `4->9->1` represents the number 491. The root-to-leaf path `4->0` represents the number 40. Therefore, sum = 495 + 491 + 40 = `1026`. 

**Constraints:**

*   The number of nodes in the tree is in the range `[1, 1000]`.
*   `0 <= Node.val <= 9`
*   The depth of the tree will not exceed `10`.

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
function sumNumbers(root: TreeNode | null): number {
    let sum = 0
    function recurseSum(node: TreeNode | null, curNum: number): void {
        if (node === null) {
            return
        }
        const newNum = 10 * curNum + node.val
        if (node.left === null && node.right === null) {
            sum += newNum
            return
        }
        if (node.left !== null) {
            recurseSum(node.left, newNum)
        }
        if (node.right !== null) {
            recurseSum(node.right, newNum)
        }
    }
    recurseSum(root, 0)
    return sum
}

export { sumNumbers }
```