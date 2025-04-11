[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 149\. Max Points on a Line

Hard

Given an array of `points` where <code>points[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> represents a point on the **X-Y** plane, return _the maximum number of points that lie on the same straight line_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane1.jpg)

**Input:** points = \[\[1,1],[2,2],[3,3]]

**Output:** 3 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane2.jpg)

**Input:** points = \[\[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]

**Output:** 4 

**Constraints:**

*   `1 <= points.length <= 300`
*   `points[i].length == 2`
*   <code>-10<sup>4</sup> <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>4</sup></code>
*   All the `points` are **unique**.

## Solution

```typescript
function maxPoints(points: number[][]): number {
    if (points.length <= 2) {
        return points.length
    }
    const map = new Map<number, number>()
    let result: number = 0
    for (let i = 0; i < points.length; i++) {
        const [x0, y0] = points[i]
        for (let j = i + 1; j < points.length; j++) {
            const [x1, y1] = points[j]
            let m: number
            if (x0 === x1) {
                m = Number.MAX_VALUE
            } else if (y0 === y1) {
                m = 0
            } else {
                m = (y0 - y1) / (x0 - x1)
            }
            const nextM: number = map.has(m) ? map.get(m) + 1 : 2
            map.set(m, nextM)
            result = Math.max(result, nextM)
        }
        map.clear()
    }
    return result
}

export { maxPoints }
```