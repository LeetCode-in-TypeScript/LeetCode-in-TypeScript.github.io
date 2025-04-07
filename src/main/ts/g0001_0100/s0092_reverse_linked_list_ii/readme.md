[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 92\. Reverse Linked List II

Medium

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

**Input:** head = [1,2,3,4,5], left = 2, right = 4

**Output:** [1,4,3,2,5] 

**Example 2:**

**Input:** head = [5], left = 1, right = 1

**Output:** [5] 

**Constraints:**

*   The number of nodes in the list is `n`.
*   `1 <= n <= 500`
*   `-500 <= Node.val <= 500`
*   `1 <= left <= right <= n`

**Follow up:** Could you do it in one pass?

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
function reverseBetween(head: ListNode | null, left: number, right: number): ListNode | null {
    if (left === right || head === null) {
        return head
    }
    let prev: ListNode | null = null
    let temp: ListNode | null = head
    let k = left
    while (temp !== null && k > 1) {
        prev = temp
        temp = temp.next
        k--
    }
    const start = temp
    let prev1: ListNode | null = null
    let tail: ListNode | null = temp
    for (let i = 0; i <= right - left && tail !== null; i++) {
        const next = tail.next
        tail.next = prev1
        prev1 = tail
        tail = next
    }
    if (prev !== null) {
        prev.next = prev1
    } else {
        head = prev1
    }
    if (start !== null) {
        start.next = tail
    }
    return head
}

export { reverseBetween }
```