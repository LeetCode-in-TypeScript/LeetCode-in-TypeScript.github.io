[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 290\. Word Pattern

Easy

Given a `pattern` and a string `s`, find if `s` follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `s`.

**Example 1:**

**Input:** pattern = "abba", s = "dog cat cat dog"

**Output:** true 

**Example 2:**

**Input:** pattern = "abba", s = "dog cat cat fish"

**Output:** false 

**Example 3:**

**Input:** pattern = "aaaa", s = "dog cat cat dog"

**Output:** false 

**Example 4:**

**Input:** pattern = "abba", s = "dog dog dog dog"

**Output:** false 

**Constraints:**

*   `1 <= pattern.length <= 300`
*   `pattern` contains only lower-case English letters.
*   `1 <= s.length <= 3000`
*   `s` contains only lower-case English letters and spaces `' '`.
*   `s` **does not contain** any leading or trailing spaces.
*   All the words in `s` are separated by a **single space**.

## Solution

```typescript
function wordPattern(pattern: string, s: string): boolean {
    const map = new Map<string, string>()
    const words = s.split(' ')
    if (words.length !== pattern.length) {
        return false
    }
    for (let i = 0; i < pattern.length; i++) {
        const char = pattern[i]
        const word = words[i]
        if (!map.has(char)) {
            if ([...map.values()].includes(word)) {
                return false
            }
            map.set(char, word)
        } else {
            if (map.get(char) !== word) {
                return false
            }
        }
    }
    return true
}

export { wordPattern }
```