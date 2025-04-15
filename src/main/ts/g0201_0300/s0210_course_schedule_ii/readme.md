[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 210\. Course Schedule II

Medium

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.

*   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return _the ordering of courses you should take to finish all courses_. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

**Example 1:**

**Input:** numCourses = 2, prerequisites = \[\[1,0]]

**Output:** [0,1]

**Explanation:**

    There are a total of 2 courses to take. To take course 1 you should have finished course 0.
    So the correct course order is [0,1].

**Example 2:**

**Input:** numCourses = 4, prerequisites = \[\[1,0],[2,0],[3,1],[3,2]]

**Output:** [0,2,1,3]

**Explanation:**

    There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
    So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].

**Example 3:**

**Input:** numCourses = 1, prerequisites = []

**Output:** [0] 

**Constraints:**

*   `1 <= numCourses <= 2000`
*   `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
*   `prerequisites[i].length == 2`
*   <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
*   <code>a<sub>i</sub> != b<sub>i</sub></code>
*   All the pairs <code>[a<sub>i</sub>, b<sub>i</sub>]</code> are **distinct**.

## Solution

```typescript
function findOrder(numCourses: number, prerequisites: number[][]): number[] {
    let sortedOrder: number[] = []
    if (numCourses < 0) return sortedOrder
    let inDegree = new Array(numCourses).fill(0),
        graph = new Array(numCourses).fill(0).map(() => new Array()),
        source = new Array<number>()
    prerequisites.forEach((course: number[]) => {
        graph[course[1]].push(course[0])
        inDegree[course[0]]++
    })
    inDegree.forEach((value: number, index: number) => {
        if (value === 0) {
            source.push(index)
        }
    })
    while (source.length > 0) {
        const course = source.shift()
        if (course === undefined) break
        sortedOrder.push(course)
        graph[course].forEach((val) => {
            inDegree[val]--
            if (inDegree[val] === 0) {
                source.push(val)
            }
        })
    }
    return sortedOrder.length === numCourses ? sortedOrder : []
}

export { findOrder }
```