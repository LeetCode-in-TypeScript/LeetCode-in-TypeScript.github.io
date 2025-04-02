[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 14\. Longest Common Prefix

Easy

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

**Input:** strs = ["flower","flow","flight"]

**Output:** "fl" 

**Example 2:**

**Input:** strs = ["dog","racecar","car"]

**Output:** ""

**Explanation:** There is no common prefix among the input strings. 

**Constraints:**

*   `1 <= strs.length <= 200`
*   `0 <= strs[i].length <= 200`
*   `strs[i]` consists of only lower-case English letters.

## Solution

```typescript
function longestCommonPrefix(strs: string[]): string {
    if (strs.length < 1) {
        return ''
    }
    if (strs.length === 1) {
        return strs[0]
    }
    let temp = strs[0]
    let i = 1
    let cur: string
    while (temp.length > 0 && i < strs.length) {
        if (temp.length > strs[i].length) {
            temp = temp.substring(0, strs[i].length)
        }
        cur = strs[i].substring(0, temp.length)
        if (cur !== temp) {
            temp = temp.substring(0, temp.length - 1)
        } else {
            i++
        }
    }
    return temp
}

export { longestCommonPrefix }
```