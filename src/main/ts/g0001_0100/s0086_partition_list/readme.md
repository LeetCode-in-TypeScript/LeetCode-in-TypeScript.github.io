[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 86\. Partition List

Medium

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

**Input:** head = [1,4,3,2,5,2], x = 3

**Output:** [1,2,2,4,3,5] 

**Example 2:**

**Input:** head = [2,1], x = 2

**Output:** [1,2] 

**Constraints:**

*   The number of nodes in the list is in the range `[0, 200]`.
*   `-100 <= Node.val <= 100`
*   `-200 <= x <= 200`

## Solution

```typescript
import { ListNode } from '../../com_github_leetcode/listnode'

/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */
function partition(head: ListNode | null, x: number): ListNode | null {
    let beforeHead = new ListNode(0)
    let afterHead = new ListNode(0)
    let before = beforeHead
    let after = afterHead
    while (head !== null) {
        const nextNode = head.next
        if (head.val < x) {
            before.next = head
            before = before.next
        } else {
            after.next = head
            after = after.next
        }
        head = nextNode
    }
    after.next = null
    before.next = afterHead.next
    return beforeHead.next
}

export { partition }
```