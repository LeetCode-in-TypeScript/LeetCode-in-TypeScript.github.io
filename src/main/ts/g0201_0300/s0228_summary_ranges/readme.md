[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 228\. Summary Ranges

Easy

You are given a **sorted unique** integer array `nums`.

Return _the **smallest sorted** list of ranges that **cover all the numbers in the array exactly**_. That is, each element of `nums` is covered by exactly one of the ranges, and there is no integer `x` such that `x` is in one of the ranges but not in `nums`.

Each range `[a,b]` in the list should be output as:

*   `"a->b"` if `a != b`
*   `"a"` if `a == b`

**Example 1:**

**Input:** nums = [0,1,2,4,5,7]

**Output:** ["0->2","4->5","7"]

**Explanation:** The ranges are: [0,2] --> "0->2" [4,5] --> "4->5" [7,7] --> "7" 

**Example 2:**

**Input:** nums = [0,2,3,4,6,8,9]

**Output:** ["0","2->4","6","8->9"]

**Explanation:** The ranges are: [0,0] --> "0" [2,4] --> "2->4" [6,6] --> "6" [8,9] --> "8->9" 

**Example 3:**

**Input:** nums = []

**Output:** [] 

**Example 4:**

**Input:** nums = [-1]

**Output:** ["-1"] 

**Example 5:**

**Input:** nums = [0]

**Output:** ["0"] 

**Constraints:**

*   `0 <= nums.length <= 20`
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>
*   All the values of `nums` are **unique**.
*   `nums` is sorted in ascending order.

## Solution

```typescript
function summaryRanges(nums: number[]): string[] {
    const ranges: string[] = []
    const n = nums.length
    if (n === 0) {
        return ranges
    }
    let a = nums[0]
    let b = a
    let strB = ''
    for (let i = 1; i < n; i++) {
        if (nums[i] !== b + 1) {
            strB = a.toString()
            if (a !== b) {
                strB += '->' + b.toString()
            }
            ranges.push(strB)
            a = nums[i]
            b = a
            strB = ''
        } else {
            b++
        }
    }
    strB = a.toString()
    if (a !== b) {
        strB += '->' + b.toString()
    }
    ranges.push(strB)
    return ranges
}

export { summaryRanges }
```