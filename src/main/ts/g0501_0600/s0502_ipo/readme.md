[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 502\. IPO

Hard

Suppose LeetCode will start its **IPO** soon. In order to sell a good price of its shares to Venture Capital, LeetCode would like to work on some projects to increase its capital before the **IPO**. Since it has limited resources, it can only finish at most `k` distinct projects before the **IPO**. Help LeetCode design the best way to maximize its total capital after finishing at most `k` distinct projects.

You are given `n` projects where the <code>i<sup>th</sup></code> project has a pure profit `profits[i]` and a minimum capital of `capital[i]` is needed to start it.

Initially, you have `w` capital. When you finish a project, you will obtain its pure profit and the profit will be added to your total capital.

Pick a list of **at most** `k` distinct projects from given projects to **maximize your final capital**, and return _the final maximized capital_.

The answer is guaranteed to fit in a 32-bit signed integer.

**Example 1:**

**Input:** k = 2, w = 0, profits = [1,2,3], capital = [0,1,1]

**Output:** 4

**Explanation:** 

Since your initial capital is 0, you can only start the project indexed 0. 

After finishing it you will obtain profit 1 and your capital becomes 1. 

With capital 1, you can either start the project indexed 1 or the project indexed 2. 

Since you can choose at most 2 projects, you need to finish the project indexed 2 to get the maximum capital. 

Therefore, output the final maximized capital, which is 0 + 1 + 3 = 4.

**Example 2:**

**Input:** k = 3, w = 0, profits = [1,2,3], capital = [0,1,2]

**Output:** 6

**Constraints:**

*   <code>1 <= k <= 10<sup>5</sup></code>
*   <code>0 <= w <= 10<sup>9</sup></code>
*   `n == profits.length`
*   `n == capital.length`
*   <code>1 <= n <= 10<sup>5</sup></code>
*   <code>0 <= profits[i] <= 10<sup>4</sup></code>
*   <code>0 <= capital[i] <= 10<sup>9</sup></code>

## Solution

```typescript
class MaxHeap {
    private heap: number[]

    constructor() {
        this.heap = []
    }

    push(value: number) {
        this.heap.push(value)
        this.heapifyUp()
    }

    pop(): number | undefined {
        if (this.heap.length === 0) {
            return undefined
        }
        if (this.heap.length === 1) {
            return this.heap.pop()
        }
        const max = this.heap[0]
        this.heap[0] = this.heap.pop()!
        this.heapifyDown()
        return max
    }

    isEmpty(): boolean {
        return this.heap.length === 0
    }

    private heapifyUp() {
        let index = this.heap.length - 1
        while (index > 0) {
            let parentIndex = Math.floor((index - 1) / 2)
            if (this.heap[parentIndex] >= this.heap[index]) {
                break
            }
            ;[this.heap[parentIndex], this.heap[index]] = [this.heap[index], this.heap[parentIndex]]
            index = parentIndex
        }
    }

    private heapifyDown() {
        let index = 0
        while (true) {
            let left = 2 * index + 1
            let right = 2 * index + 2
            let largest = index
            if (left < this.heap.length && this.heap[left] > this.heap[largest]) {
                largest = left
            }
            if (right < this.heap.length && this.heap[right] > this.heap[largest]) {
                largest = right
            }
            if (largest === index) {
                break
            }
            ;[this.heap[index], this.heap[largest]] = [this.heap[largest], this.heap[index]]
            index = largest
        }
    }
}

function findMaximizedCapital(k: number, w: number, profits: number[], capital: number[]): number {
    let projects: [number, number][] = []
    const n = profits.length
    for (let i = 0; i < n; i++) {
        projects.push([capital[i], profits[i]])
    }
    projects.sort((a, b) => a[0] - b[0])
    const maxHeap = new MaxHeap()
    let i = 0
    while (k--) {
        while (i < n && projects[i][0] <= w) {
            maxHeap.push(projects[i][1])
            i++
        }
        if (maxHeap.isEmpty()) {
            break
        }
        w += maxHeap.pop()!
    }
    return w
}

export { findMaximizedCapital }
```