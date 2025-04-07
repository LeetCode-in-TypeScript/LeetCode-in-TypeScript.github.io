[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 67\. Add Binary

Easy

Given two binary strings `a` and `b`, return _their sum as a binary string_.

**Example 1:**

**Input:** a = "11", b = "1"

**Output:** "100" 

**Example 2:**

**Input:** a = "1010", b = "1011"

**Output:** "10101" 

**Constraints:**

*   <code>1 <= a.length, b.length <= 10<sup>4</sup></code>
*   `a` and `b` consist only of `'0'` or `'1'` characters.
*   Each string does not contain leading zeros except for the zero itself.

## Solution

```typescript
function addBinary(a: string, b: string): string {
    const aArray = a.split('')
    const bArray = b.split('')
    let sb: string[] = []
    let i = aArray.length - 1
    let j = bArray.length - 1
    let carry = 0
    while (i >= 0 || j >= 0) {
        const digitA = i >= 0 ? parseInt(aArray[i]) : 0
        const digitB = j >= 0 ? parseInt(bArray[j]) : 0
        const sum = digitA + digitB + carry
        sb.push((sum % 2).toString())
        carry = Math.floor(sum / 2)
        i--
        j--
    }
    if (carry !== 0) {
        sb.push(carry.toString())
    }
    return sb.reverse().join('')
}

export { addBinary }
```