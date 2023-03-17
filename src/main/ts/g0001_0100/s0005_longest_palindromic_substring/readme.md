[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest_ _palindromic_ _substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab"

**Explanation:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```typescript
function longestPalindrome(s: string): string {
    let max = 0
    let res = ''
    for (let i = 0; i < s.length; i++) {
        for (let j = i + 1; j <= s.length; j++) {
            if (s.slice(i, j).length > max && isPalindrome(s.slice(i, j))) {
                max = s.slice(i, j).length
                res = s.slice(i, j)
            }
        }
    }
    return res
}

const isPalindrome = (s: string): boolean => {
    let i = 0
    let j = s.length - 1
    while (i < j) {
        if (s[i] !== s[j]) {
            return false
        }
        i++
        j--
    }
    return true
}

export { longestPalindrome }
```