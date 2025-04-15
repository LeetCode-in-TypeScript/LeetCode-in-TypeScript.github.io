[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 373\. Find K Pairs with Smallest Sums

Medium

You are given two integer arrays `nums1` and `nums2` sorted in **ascending order** and an integer `k`.

Define a pair `(u, v)` which consists of one element from the first array and one element from the second array.

Return _the_ `k` _pairs_ <code>(u<sub>1</sub>, v<sub>1</sub>), (u<sub>2</sub>, v<sub>2</sub>), ..., (u<sub>k</sub>, v<sub>k</sub>)</code> _with the smallest sums_.

**Example 1:**

**Input:** nums1 = [1,7,11], nums2 = [2,4,6], k = 3

**Output:** [[1,2],[1,4],[1,6]]

**Explanation:** The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]

**Example 2:**

**Input:** nums1 = [1,1,2], nums2 = [1,2,3], k = 2

**Output:** [[1,1],[1,1]]

**Explanation:** The first 2 pairs are returned from the sequence: [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]

**Example 3:**

**Input:** nums1 = [1,2], nums2 = [3], k = 3

**Output:** [[1,3],[2,3]]

**Explanation:** All possible pairs are returned from the sequence: [1,3],[2,3]

**Constraints:**

*   <code>1 <= nums1.length, nums2.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums1[i], nums2[i] <= 10<sup>9</sup></code>
*   `nums1` and `nums2` both are sorted in **ascending order**.
*   `1 <= k <= 1000`

## Solution

```typescript
class MinHeap {
    private heap: { sum: number; i: number; j: number }[]

    constructor() {
        this.heap = []
    }

    push(val: { sum: number; i: number; j: number }) {
        this.heap.push(val)
        this.bubbleUp()
    }

    pop(): { sum: number; i: number; j: number } | undefined {
        if (this.heap.length === 0) {
            return undefined
        }
        if (this.heap.length === 1) {
            return this.heap.pop()
        }
        const min = this.heap[0]
        this.heap[0] = this.heap.pop()!
        this.bubbleDown()
        return min
    }

    isEmpty(): boolean {
        return this.heap.length === 0
    }

    private bubbleUp() {
        let index = this.heap.length - 1
        while (index > 0) {
            let parentIndex = Math.floor((index - 1) / 2)
            if (this.heap[parentIndex].sum <= this.heap[index].sum) {
                break
            }
            ;[this.heap[parentIndex], this.heap[index]] = [this.heap[index], this.heap[parentIndex]]
            index = parentIndex
        }
    }

    private bubbleDown() {
        let index = 0
        let length = this.heap.length
        while (true) {
            let leftChildIndex = 2 * index + 1
            let rightChildIndex = 2 * index + 2
            let smallest = index
            if (leftChildIndex < length && this.heap[leftChildIndex].sum < this.heap[smallest].sum) {
                smallest = leftChildIndex
            }
            if (rightChildIndex < length && this.heap[rightChildIndex].sum < this.heap[smallest].sum) {
                smallest = rightChildIndex
            }
            if (smallest === index) {
                break
            }
            ;[this.heap[index], this.heap[smallest]] = [this.heap[smallest], this.heap[index]]
            index = smallest
        }
    }
}

function kSmallestPairs(nums1: number[], nums2: number[], k: number): number[][] {
    let ans: number[][] = []
    if (nums1.length === 0 || nums2.length === 0 || k === 0) {
        return ans
    }
    let minHeap = new MinHeap()
    for (let i = 0; i < Math.min(nums1.length, k); i++) {
        minHeap.push({ sum: nums1[i] + nums2[0], i, j: 0 })
    }
    while (k-- > 0 && !minHeap.isEmpty()) {
        let { i, j } = minHeap.pop()!
        ans.push([nums1[i], nums2[j]])
        if (j + 1 < nums2.length) {
            minHeap.push({ sum: nums1[i] + nums2[j + 1], i, j: j + 1 })
        }
    }
    return ans
}

export { kSmallestPairs }
```