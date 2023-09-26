[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 23\. Merge k Sorted Lists

Hard

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

**Input:** lists = \[\[1,4,5],[1,3,4],[2,6]]

**Output:** [1,1,2,3,4,4,5,6]

**Explanation:** The linked-lists are: [ 1->4->5, 1->3->4, 2->6 ] merging them into one sorted list: 1->1->2->3->4->4->5->6 

**Example 2:**

**Input:** lists = []

**Output:** [] 

**Example 3:**

**Input:** lists = \[\[]]

**Output:** [] 

**Constraints:**

*   `k == lists.length`
*   `0 <= k <= 10^4`
*   `0 <= lists[i].length <= 500`
*   `-10^4 <= lists[i][j] <= 10^4`
*   `lists[i]` is sorted in **ascending order**.
*   The sum of `lists[i].length` won't exceed `10^4`.

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
function mergeKLists(lists: Array<ListNode | null>): ListNode | null {
    if (lists.length === 0) {
        return null
    }
    return mergeKListsRecursive(lists, 0, lists.length)
}

function mergeKListsRecursive(lists: Array<ListNode | null>, leftIndex: number, rightIndex: number): ListNode | null {
    if (rightIndex > leftIndex + 1) {
        const mid = Math.floor((leftIndex + rightIndex) / 2)
        const left = mergeKListsRecursive(lists, leftIndex, mid)
        const right = mergeKListsRecursive(lists, mid, rightIndex)
        return mergeTwoLists(left, right)
    } else {
        return lists[leftIndex]
    }
}

function mergeTwoLists(left: ListNode | null, right: ListNode | null): ListNode | null {
    if (left === null) {
        return right
    }
    if (right === null) {
        return left
    }
    let res: ListNode | null
    if (left.val <= right.val) {
        res = left
        left = left.next
    } else {
        res = right
        right = right.next
    }
    let node = res
    while (left !== null || right !== null) {
        if (right === null || left.val <= right.val) {
            node.next = left
            left = left.next
        } else {
            node.next = right
            right = right.next
        }
        node = node.next
    }
    return res
}

export { mergeKLists }
```