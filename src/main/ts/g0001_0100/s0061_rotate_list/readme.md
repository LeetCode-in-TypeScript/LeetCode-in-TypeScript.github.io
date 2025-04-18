[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 61\. Rotate List

Medium

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

**Input:** head = [1,2,3,4,5], k = 2

**Output:** [4,5,1,2,3] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

**Input:** head = [0,1,2], k = 4

**Output:** [2,0,1] 

**Constraints:**

*   The number of nodes in the list is in the range `[0, 500]`.
*   `-100 <= Node.val <= 100`
*   <code>0 <= k <= 2 * 10<sup>9</sup></code>

## Solution

```typescript
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
function rotateRight(head: ListNode | null, k: number): ListNode | null {
    if (!head || k === 0) {
        return head
    }
    let tail: ListNode | null = head
    let count = 1
    while (tail.next) {
        count++
        tail = tail.next
    }
    let times = k % count
    if (times === 0) {
        return head
    }
    let temp: ListNode | null = head
    for (let i = 1; i < count - times; i++) {
        temp = temp!.next
    }
    let newHead = temp!.next
    temp!.next = null
    tail!.next = head
    return newHead
}

export { rotateRight }
```