[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 106\. Construct Binary Tree from Inorder and Postorder Traversal

Medium

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]

**Output:** [3,9,20,null,null,15,7] 

**Example 2:**

**Input:** inorder = [-1], postorder = [-1]

**Output:** [-1] 

**Constraints:**

*   `1 <= inorder.length <= 3000`
*   `postorder.length == inorder.length`
*   `-3000 <= inorder[i], postorder[i] <= 3000`
*   `inorder` and `postorder` consist of **unique** values.
*   Each value of `postorder` also appears in `inorder`.
*   `inorder` is **guaranteed** to be the inorder traversal of the tree.
*   `postorder` is **guaranteed** to be the postorder traversal of the tree.

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
function buildTree(inorder: number[], postorder: number[]): TreeNode | null {
    const inIndex: number[] = [inorder.length - 1]
    const postIndex: number[] = [postorder.length - 1]
    return helper(inorder, postorder, inIndex, postIndex, Number.MAX_VALUE)
}

function helper(
    inorder: number[],
    postorder: number[],
    inIndex: number[],
    postIndex: number[],
    target: number,
): TreeNode | null {
    if (inIndex[0] < 0 || inorder[inIndex[0]] === target) {
        return null
    }
    const root = new TreeNode(postorder[postIndex[0]--])
    root.right = helper(inorder, postorder, inIndex, postIndex, root.val)
    inIndex[0]--
    root.left = helper(inorder, postorder, inIndex, postIndex, target)
    return root
}

export { buildTree }
```