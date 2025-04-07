[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 82\. Remove Duplicates from Sorted List II

Medium

Given the `head` of a sorted linked list, _delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list_. Return _the linked list **sorted** as well_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

**Input:** head = [1,2,3,3,4,4,5]

**Output:** [1,2,5] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

**Input:** head = [1,1,1,2,3]

**Output:** [2,3] 

**Constraints:**

*   The number of nodes in the list is in the range `[0, 300]`.
*   `-100 <= Node.val <= 100`
*   The list is guaranteed to be **sorted** in ascending order.

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
function deleteDuplicates(head: ListNode | null): ListNode | null {
    if (!head || !head.next) {
        return head
    }
    const dummy = new ListNode(0)
    dummy.next = head
    let prev: ListNode = dummy
    let curr: ListNode | null = head
    while (curr) {
        let hasDuplicate = false
        while (curr.next && curr.val === curr.next.val) {
            hasDuplicate = true
            curr = curr.next
        }
        if (hasDuplicate) {
            prev.next = curr.next
        } else {
            prev = prev.next!
        }
        curr = curr.next
    }
    return dummy.next
}

export { deleteDuplicates }
```