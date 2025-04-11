[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 205\. Isomorphic Strings

Easy

Given two strings `s` and `t`, _determine if they are isomorphic_.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1:**

**Input:** s = "egg", t = "add"

**Output:** true 

**Example 2:**

**Input:** s = "foo", t = "bar"

**Output:** false 

**Example 3:**

**Input:** s = "paper", t = "title"

**Output:** true 

**Constraints:**

*   <code>1 <= s.length <= 5 * 10<sup>4</sup></code>
*   `t.length == s.length`
*   `s` and `t` consist of any valid ascii character.

## Solution

```typescript
function isIsomorphic(s: string, t: string): boolean {
    if (s.length !== t.length) {
        return false
    }
    const mapS = new Map<string, string>()
    const mapT = new Map<string, string>()
    for (let i = 0; i < s.length; i++) {
        if (mapS.has(s[i]) || mapT.has(t[i])) {
            if (mapS.get(s[i]) !== t[i] || mapT.get(t[i]) !== s[i]) {
                return false
            }
        } else {
            mapS.set(s[i], t[i])
            mapT.set(t[i], s[i])
        }
    }
    return true
}

export { isIsomorphic }
```