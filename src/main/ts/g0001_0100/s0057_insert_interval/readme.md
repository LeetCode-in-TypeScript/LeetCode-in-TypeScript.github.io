[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 57\. Insert Interval

Medium

You are given an array of non-overlapping intervals `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represent the start and the end of the <code>i<sup>th</sup></code> interval and `intervals` is sorted in ascending order by <code>start<sub>i</sub></code>. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by <code>start<sub>i</sub></code> and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` _after the insertion_.

**Example 1:**

**Input:** intervals = \[\[1,3],[6,9]], newInterval = [2,5]

**Output:** [[1,5],[6,9]] 

**Example 2:**

**Input:** intervals = \[\[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]

**Output:** [[1,2],[3,10],[12,16]]

**Explanation:** Because the new interval `[4,8]` overlaps with `[3,5],[6,7],[8,10]`.

**Example 3:**

**Input:** intervals = [], newInterval = [5,7]

**Output:** [[5,7]] 

**Example 4:**

**Input:** intervals = \[\[1,5]], newInterval = [2,3]

**Output:** [[1,5]] 

**Example 5:**

**Input:** intervals = \[\[1,5]], newInterval = [2,7]

**Output:** [[1,7]] 

**Constraints:**

*   <code>0 <= intervals.length <= 10<sup>4</sup></code>
*   `intervals[i].length == 2`
*   <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>5</sup></code>
*   `intervals` is sorted by <code>start<sub>i</sub></code> in **ascending** order.
*   `newInterval.length == 2`
*   <code>0 <= start <= end <= 10<sup>5</sup></code>

## Solution

```typescript
function insert(intervals: number[][], newInterval: number[]): number[][] {
    const n = intervals.length
    let l = 0
    let r = n - 1
    while (l < n && newInterval[0] > intervals[l][1]) {
        l++
    }
    while (r >= 0 && newInterval[1] < intervals[r][0]) {
        r--
    }
    const res: number[][] = new Array(l + n - r).fill(0).map(() => new Array(2))
    for (let i = 0; i < l; i++) {
        res[i] = [...intervals[i]]
    }
    res[l] = [
        Math.min(newInterval[0], l === n ? newInterval[0] : intervals[l][0]),
        Math.max(newInterval[1], r === -1 ? newInterval[1] : intervals[r][1]),
    ]
    for (let i = l + 1, j = r + 1; j < n; i++, j++) {
        res[i] = intervals[j]
    }
    return res
}

export { insert }
```