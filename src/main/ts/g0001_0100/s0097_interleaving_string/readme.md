[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 97\. Interleaving String

Medium

Given strings `s1`, `s2`, and `s3`, find whether `s3` is formed by an **interleaving** of `s1` and `s2`.

An **interleaving** of two strings `s` and `t` is a configuration where they are divided into **non-empty** substrings such that:

*   <code>s = s<sub>1</sub> + s<sub>2</sub> + ... + s<sub>n</sub></code>
*   <code>t = t<sub>1</sub> + t<sub>2</sub> + ... + t<sub>m</sub></code>
*   `|n - m| <= 1`
*   The **interleaving** is <code>s<sub>1</sub> + t<sub>1</sub> + s<sub>2</sub> + t<sub>2</sub> + s<sub>3</sub> + t<sub>3</sub> + ...</code> or <code>t<sub>1</sub> + s<sub>1</sub> + t<sub>2</sub> + s<sub>2</sub> + t<sub>3</sub> + s<sub>3</sub> + ...</code>

**Note:** `a + b` is the concatenation of strings `a` and `b`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

**Input:** s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"

**Output:** true 

**Example 2:**

**Input:** s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"

**Output:** false 

**Example 3:**

**Input:** s1 = "", s2 = "", s3 = ""

**Output:** true 

**Constraints:**

*   `0 <= s1.length, s2.length <= 100`
*   `0 <= s3.length <= 200`
*   `s1`, `s2`, and `s3` consist of lowercase English letters.

**Follow up:** Could you solve it using only `O(s2.length)` additional memory space?

## Solution

```typescript
function isInterleave(s1: string, s2: string, s3: string): boolean {
    if (s3.length !== s1.length + s2.length) {
        return false
    }
    const cache: boolean[][] = Array.from({ length: s1.length + 1 }, () => Array(s2.length + 1).fill(null))
    return isInterleaveHelper(s1, s2, s3, 0, 0, 0, cache)
}

function isInterleaveHelper(
    s1: string,
    s2: string,
    s3: string,
    i1: number,
    i2: number,
    i3: number,
    cache: boolean[][],
): boolean {
    if (cache[i1][i2] !== null) {
        return cache[i1][i2]
    }
    if (i1 === s1.length && i2 === s2.length && i3 === s3.length) {
        return true
    }
    let result = false
    if (i1 < s1.length && s1.charAt(i1) === s3.charAt(i3)) {
        result = isInterleaveHelper(s1, s2, s3, i1 + 1, i2, i3 + 1, cache)
    }
    if (i2 < s2.length && s2.charAt(i2) === s3.charAt(i3)) {
        result = result || isInterleaveHelper(s1, s2, s3, i1, i2 + 1, i3 + 1, cache)
    }
    cache[i1][i2] = result
    return result
}

export { isInterleave }
```