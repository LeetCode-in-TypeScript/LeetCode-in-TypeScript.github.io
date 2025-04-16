[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 399\. Evaluate Division

Medium

You are given an array of variable pairs `equations` and an array of real numbers `values`, where <code>equations[i] = [A<sub>i</sub>, B<sub>i</sub>]</code> and `values[i]` represent the equation <code>A<sub>i</sub> / B<sub>i</sub> = values[i]</code>. Each <code>A<sub>i</sub></code> or <code>B<sub>i</sub></code> is a string that represents a single variable.

You are also given some `queries`, where <code>queries[j] = [C<sub>j</sub>, D<sub>j</sub>]</code> represents the <code>j<sup>th</sup></code> query where you must find the answer for <code>C<sub>j</sub> / D<sub>j</sub> = ?</code>.

Return _the answers to all queries_. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Example 1:**

**Input:** equations = \[\["a","b"],["b","c"]], values = [2.0,3.0], queries = \[\["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]

**Output:** [6.00000,0.50000,-1.00000,1.00000,-1.00000]

**Explanation:**

Given: _a / b = 2.0_, _b / c = 3.0_

queries are: _a / c = ?_, _b / a = ?_, _a / e = ?_, _a / a = ?_, _x / x = ?_

return: [6.0, 0.5, -1.0, 1.0, -1.0 ]

**Example 2:**

**Input:** equations = \[\["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = \[\["a","c"],["c","b"],["bc","cd"],["cd","bc"]]

**Output:** [3.75000,0.40000,5.00000,0.20000]

**Example 3:**

**Input:** equations = \[\["a","b"]], values = [0.5], queries = \[\["a","b"],["b","a"],["a","c"],["x","y"]]

**Output:** [0.50000,2.00000,-1.00000,-1.00000]

**Constraints:**

*   `1 <= equations.length <= 20`
*   `equations[i].length == 2`
*   <code>1 <= A<sub>i</sub>.length, B<sub>i</sub>.length <= 5</code>
*   `values.length == equations.length`
*   `0.0 < values[i] <= 20.0`
*   `1 <= queries.length <= 20`
*   `queries[i].length == 2`
*   <code>1 <= C<sub>j</sub>.length, D<sub>j</sub>.length <= 5</code>
*   <code>A<sub>i</sub>, B<sub>i</sub>, C<sub>j</sub>, D<sub>j</sub></code> consist of lower case English letters and digits.

## Solution

```typescript
type MapType = Map<string, string>
type RateType = Map<string, number>

function calcEquation(equations: [string, string][], values: number[], queries: [string, string][]): number[] {
    const root: MapType = new Map()
    const rate: RateType = new Map()
    for (const [x, y] of equations) {
        if (!root.has(x)) {
            root.set(x, x)
            rate.set(x, 1.0)
        }
        if (!root.has(y)) {
            root.set(y, y)
            rate.set(y, 1.0)
        }
    }
    for (let i = 0; i < equations.length; ++i) {
        const [x, y] = equations[i]
        union(x, y, values[i], root, rate)
    }
    const result: number[] = []
    for (const [x, y] of queries) {
        if (!root.has(x) || !root.has(y)) {
            result.push(-1.0)
        } else {
            const rootX = findRoot(x, x, 1.0, root, rate)
            const rootY = findRoot(y, y, 1.0, root, rate)
            if (rootX === rootY) {
                result.push(rate.get(x)! / rate.get(y)!)
            } else {
                result.push(-1.0)
            }
        }
    }
    return result
}

function union(x: string, y: string, value: number, root: MapType, rate: RateType): void {
    const rootX = findRoot(x, x, 1.0, root, rate)
    const rootY = findRoot(y, y, 1.0, root, rate)

    if (rootX !== rootY) {
        root.set(rootX, rootY)
        const rateX = rate.get(x)!
        const rateY = rate.get(y)!
        rate.set(rootX, (value * rateY) / rateX)
    }
}

function findRoot(originalX: string, x: string, rateSoFar: number, root: MapType, rate: RateType): string {
    if (root.get(x) === x) {
        root.set(originalX, x)
        rate.set(originalX, rateSoFar * rate.get(x)!)
        return x
    }
    return findRoot(originalX, root.get(x)!, rateSoFar * rate.get(x)!, root, rate)
}

export { calcEquation }
```