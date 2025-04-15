[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 392\. Is Subsequence

Easy

Given two strings `s` and `t`, return `true` _if_ `s` _is a **subsequence** of_ `t`_, or_ `false` _otherwise_.

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

**Example 1:**

**Input:** s = "abc", t = "ahbgdc"

**Output:** true

**Example 2:**

**Input:** s = "axc", t = "ahbgdc"

**Output:** false

**Constraints:**

*   `0 <= s.length <= 100`
*   <code>0 <= t.length <= 10<sup>4</sup></code>
*   `s` and `t` consist only of lowercase English letters.

**Follow up:** Suppose there are lots of incoming `s`, say <code>s<sub>1</sub>, s<sub>2</sub>, ..., s<sub>k</sub></code> where <code>k >= 10<sup>9</sup></code>, and you want to check one by one to see if `t` has its subsequence. In this scenario, how would you change your code?

## Solution

```typescript
function isSubsequence(s: string, t: string): boolean {
    let i = 0
    let j = 0
    const m = s.length
    const n = t.length
    if (m === 0) {
        return true
    }
    while (j < n) {
        if (s[i] === t[j]) {
            i++
            if (i === m) {
                return true
            }
        }
        j++
    }
    return false
}

export { isSubsequence }
```