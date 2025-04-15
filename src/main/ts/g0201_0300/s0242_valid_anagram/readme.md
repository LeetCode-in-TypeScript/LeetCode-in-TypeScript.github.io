[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 242\. Valid Anagram

Easy

Given two strings `s` and `t`, return `true` _if_ `t` _is an anagram of_ `s`_, and_ `false` _otherwise_.

**Example 1:**

**Input:** s = "anagram", t = "nagaram"

**Output:** true 

**Example 2:**

**Input:** s = "rat", t = "car"

**Output:** false 

**Constraints:**

*   <code>1 <= s.length, t.length <= 5 * 10<sup>4</sup></code>
*   `s` and `t` consist of lowercase English letters.

**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Solution

```typescript
function isAnagram(s: string, t: string): boolean {
    if (s.length !== t.length) {
        return false
    }
    let counts = new Array(26).fill(0)
    for (let i = 0; i < s.length; ++i) {
        counts[s.charCodeAt(i) - 'a'.charCodeAt(0)]++
        counts[t.charCodeAt(i) - 'a'.charCodeAt(0)]--
    }
    return counts.every((c) => c === 0)
}

export { isAnagram }
```