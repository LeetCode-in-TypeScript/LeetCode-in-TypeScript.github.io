[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 295\. Find Median from Data Stream

Hard

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

*   For example, for `arr = [2,3,4]`, the median is `3`.
*   For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

*   `MedianFinder()` initializes the `MedianFinder` object.
*   `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
*   `double findMedian()` returns the median of all elements so far. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.

**Example 1:**

**Input**

    ["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
    [[], [1], [2], [], [3], []]

**Output:** [null, null, null, 1.5, null, 2.0]

**Explanation:**

    MedianFinder medianFinder = new MedianFinder();
    medianFinder.addNum(1); // arr = [1]
    medianFinder.addNum(2); // arr = [1, 2]
    medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
    medianFinder.addNum(3); // arr[1, 2, 3]
    medianFinder.findMedian(); // return 2.0 

**Constraints:**

*   <code>-10<sup>5</sup> <= num <= 10<sup>5</sup></code>
*   There will be at least one element in the data structure before calling `findMedian`.
*   At most <code>5 * 10<sup>4</sup></code> calls will be made to `addNum` and `findMedian`.

**Follow up:**

*   If all integer numbers from the stream are in the range `[0, 100]`, how would you optimize your solution?
*   If `99%` of all integer numbers from the stream are in the range `[0, 100]`, how would you optimize your solution?

## Solution

```typescript
class MaxHeap<T> {
    private heap: T[]

    constructor() {
        this.heap = []
    }

    size(): number {
        return this.heap.length
    }

    isEmpty(): boolean {
        return this.heap.length === 0
    }

    peek(): T {
        return this.heap[0]
    }

    add(value: T): void {
        this.heap.push(value)
        this.heapifyUp()
    }

    poll(): T {
        const max = this.heap[0]
        const last = this.heap.pop()
        if (this.heap.length > 0) {
            this.heap[0] = last
            this.heapifyDown()
        }
        return max
    }

    private heapifyUp(): void {
        let currentIndex = this.heap.length - 1
        while (this.hasParent(currentIndex) && this.parent(currentIndex) < this.heap[currentIndex]) {
            const parentIndex = this.getParentIndex(currentIndex)
            this.swap(parentIndex, currentIndex)
            currentIndex = parentIndex
        }
    }

    private heapifyDown(): void {
        let currentIndex = 0
        while (this.hasLeftChild(currentIndex)) {
            let biggerChildIndex = this.getLeftChildIndex(currentIndex)
            if (this.hasRightChild(currentIndex) && this.rightChild(currentIndex) > this.leftChild(currentIndex)) {
                biggerChildIndex = this.getRightChildIndex(currentIndex)
            }

            if (this.heap[currentIndex] > this.heap[biggerChildIndex]) {
                break
            }

            this.swap(currentIndex, biggerChildIndex)
            currentIndex = biggerChildIndex
        }
    }

    private hasParent(index: number): boolean {
        return this.getParentIndex(index) >= 0
    }

    private hasLeftChild(index: number): boolean {
        return this.getLeftChildIndex(index) < this.heap.length
    }

    private hasRightChild(index: number): boolean {
        return this.getRightChildIndex(index) < this.heap.length
    }

    private parent(index: number): T {
        return this.heap[this.getParentIndex(index)]
    }

    private leftChild(index: number): T {
        return this.heap[this.getLeftChildIndex(index)]
    }

    private rightChild(index: number): T {
        return this.heap[this.getRightChildIndex(index)]
    }

    private getParentIndex(index: number): number {
        return Math.floor((index - 1) / 2)
    }

    private getLeftChildIndex(index: number): number {
        return index * 2 + 1
    }

    private getRightChildIndex(index: number): number {
        return index * 2 + 2
    }

    private swap(index1: number, index2: number): void {
        const temp = this.heap[index1]
        this.heap[index1] = this.heap[index2]
        this.heap[index2] = temp
    }
}

class MinHeap<T> {
    private heap: T[]

    constructor() {
        this.heap = []
    }

    size(): number {
        return this.heap.length
    }

    isEmpty(): boolean {
        return this.heap.length === 0
    }

    peek(): T {
        return this.heap[0]
    }

    add(value: T): void {
        this.heap.push(value)
        this.heapifyUp()
    }

    poll(): T {
        const min = this.heap[0]
        const last = this.heap.pop()
        if (this.heap.length > 0) {
            this.heap[0] = last
            this.heapifyDown()
        }
        return min
    }

    private heapifyUp(): void {
        let currentIndex = this.heap.length - 1
        while (this.hasParent(currentIndex) && this.parent(currentIndex) > this.heap[currentIndex]) {
            const parentIndex = this.getParentIndex(currentIndex)
            this.swap(parentIndex, currentIndex)
            currentIndex = parentIndex
        }
    }

    private heapifyDown(): void {
        let currentIndex = 0
        while (this.hasLeftChild(currentIndex)) {
            let smallerChildIndex = this.getLeftChildIndex(currentIndex)
            if (this.hasRightChild(currentIndex) && this.rightChild(currentIndex) < this.leftChild(currentIndex)) {
                smallerChildIndex = this.getRightChildIndex(currentIndex)
            }

            if (this.heap[currentIndex] < this.heap[smallerChildIndex]) {
                break
            }

            this.swap(currentIndex, smallerChildIndex)
            currentIndex = smallerChildIndex
        }
    }

    private hasParent(index: number): boolean {
        return this.getParentIndex(index) >= 0
    }

    private hasLeftChild(index: number): boolean {
        return this.getLeftChildIndex(index) < this.heap.length
    }

    private hasRightChild(index: number): boolean {
        return this.getRightChildIndex(index) < this.heap.length
    }

    private parent(index: number): T {
        return this.heap[this.getParentIndex(index)]
    }

    private leftChild(index: number): T {
        return this.heap[this.getLeftChildIndex(index)]
    }

    private rightChild(index: number): T {
        return this.heap[this.getRightChildIndex(index)]
    }

    private getParentIndex(index: number): number {
        return Math.floor((index - 1) / 2)
    }

    private getLeftChildIndex(index: number): number {
        return index * 2 + 1
    }

    private getRightChildIndex(index: number): number {
        return index * 2 + 2
    }

    private swap(index1: number, index2: number): void { //NOSONAR
        const temp = this.heap[index1]
        this.heap[index1] = this.heap[index2]
        this.heap[index2] = temp
    }
}

class MedianFinder {
    private maxHeap: MaxHeap<number>
    private minHeap: MinHeap<number>

    constructor() {
        this.maxHeap = new MaxHeap<number>()
        this.minHeap = new MinHeap<number>()
    }

    addNum(num: number): void {
        if (this.maxHeap.isEmpty() || num <= this.maxHeap.peek()) {
            this.maxHeap.add(num)
        } else {
            this.minHeap.add(num)
        }

        if (this.maxHeap.size() - this.minHeap.size() > 1) {
            this.minHeap.add(this.maxHeap.poll())
        } else if (this.minHeap.size() > this.maxHeap.size()) {
            this.maxHeap.add(this.minHeap.poll())
        }
    }

    findMedian(): number {
        if (this.maxHeap.size() === this.minHeap.size()) {
            return (this.maxHeap.peek() + this.minHeap.peek()) / 2
        } else {
            return this.maxHeap.size() > this.minHeap.size() ? this.maxHeap.peek() : this.minHeap.peek()
        }
    }
}

/*
 * Your MedianFinder object will be instantiated and called as such:
 * var obj = new MedianFinder()
 * obj.addNum(num)
 * var param_2 = obj.findMedian()
 */

export { MedianFinder }
```