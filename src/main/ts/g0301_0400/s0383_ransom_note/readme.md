[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 383\. Ransom Note

Easy

Given two stings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1:**

**Input:** ransomNote = "a", magazine = "b"

**Output:** false

**Example 2:**

**Input:** ransomNote = "aa", magazine = "ab"

**Output:** false

**Example 3:**

**Input:** ransomNote = "aa", magazine = "aab"

**Output:** true

**Constraints:**

*   <code>1 <= ransomNote.length, magazine.length <= 10<sup>5</sup></code>
*   `ransomNote` and `magazine` consist of lowercase English letters.

## Solution

```typescript
function canConstruct(ransomNote: string, magazine: string): boolean {
    const freq: number[] = new Array(26).fill(0)
    let remaining = ransomNote.length
    for (let i = 0; i < remaining; i++) {
        freq[ransomNote.charCodeAt(i) - 97]++
    }
    for (let i = 0; i < magazine.length && remaining > 0; i++) {
        const index = magazine.charCodeAt(i) - 97
        if (freq[index] > 0) {
            freq[index]--
            remaining--
        }
    }
    return remaining === 0
}

export { canConstruct }
```