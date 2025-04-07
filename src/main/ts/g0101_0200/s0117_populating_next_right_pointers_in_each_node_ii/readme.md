[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 117\. Populating Next Right Pointers in Each Node II

Medium

Given a binary tree

struct Node { int val; Node \*left; Node \*right; Node \*next; } 

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

**Input:** root = [1,2,3,4,5,null,7]

**Output:** [1,#,2,3,#,4,5,7,#]

**Explanation:** Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level. 

**Example 2:**

**Input:** root = []

**Output:** [] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 6000]`.
*   `-100 <= Node.val <= 100`

**Follow-up:**

*   You may only use constant extra space.
*   The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

## Solution

```typescript
import { _Node } from '../../com_github_leetcode/_node'

/**
 * Definition for _Node.
 * class _Node {
 *     val: number
 *     left: _Node | null
 *     right: _Node | null
 *     next: _Node | null
 *
 *     constructor(val?: number, left?: _Node, right?: _Node, next?: _Node) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */
function connect(root: _Node | null): _Node | null {
    if (!root) {
        return null
    }
    root.next = null
    let dummyHead = new _Node()
    let current: _Node | null = root
    while (current) {
        // reset dummyHead
        dummyHead.next = null
        let child = dummyHead
        // traverse the current level
        while (current) {
            if (current.left) {
                child.next = current.left
                child = child.next
            }
            if (current.right) {
                child.next = current.right
                child = child.next
            }
            current = current.next
        }
        // move on to the next level
        current = dummyHead.next
    }
    return root
}

export { connect }
```