[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 108\. Convert Sorted Array to Binary Search Tree

Easy

Given an integer array `nums` where the elements are sorted in **ascending order**, convert _it to a **height-balanced** binary search tree_.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

**Input:** nums = [-10,-3,0,5,9]

**Output:** [0,-3,9,-10,null,5]

**Explanation:** [0,-10,5,null,-3,null,9] is also accepted: ![](https://assets.leetcode.com/uploads/2021/02/18/btree2.jpg) 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/18/btree.jpg)

**Input:** nums = [1,3]

**Output:** [3,1]

**Explanation:** [1,3] and [3,1] are both a height-balanced BSTs. 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `nums` is sorted in a **strictly increasing** order.

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
function sortedArrayToBST(nums: number[]): TreeNode | null {
    return makeTree(nums, 0, nums.length - 1)
}

function makeTree(nums: number[], left: number, right: number): TreeNode | null {
    if (left > right) {
        return null
    }
    const mid = Math.floor((left + right) / 2)
    const midNode = new TreeNode(nums[mid])
    midNode.left = makeTree(nums, left, mid - 1)
    midNode.right = makeTree(nums, mid + 1, right)
    return midNode
}

export { sortedArrayToBST }
```