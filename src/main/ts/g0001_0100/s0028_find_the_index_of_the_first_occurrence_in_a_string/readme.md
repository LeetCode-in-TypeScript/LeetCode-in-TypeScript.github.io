[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 28\. Implement strStr()

Easy

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or `-1` if `needle` is not part of `haystack`.

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

**Example 1:**

**Input:** haystack = "hello", needle = "ll"

**Output:** 2 

**Example 2:**

**Input:** haystack = "aaaaa", needle = "bba"

**Output:** -1 

**Example 3:**

**Input:** haystack = "", needle = ""

**Output:** 0 

**Constraints:**

*   <code>0 <= haystack.length, needle.length <= 5 * 10<sup>4</sup></code>
*   `haystack` and `needle` consist of only lower-case English characters.

## Solution

```typescript
function strStr(haystack: string, needle: string): number {
    if (needle.length === 0) {
        return 0
    }
    let m = haystack.length
    let n = needle.length
    for (let start = 0; start <= m - n; start++) {
        if (haystack.substring(start, start + n) === needle) {
            return start
        }
    }
    return -1
}

export { strStr }
```