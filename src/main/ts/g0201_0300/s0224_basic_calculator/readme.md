[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 224\. Basic Calculator

Hard

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return _the result of the evaluation_.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**

**Input:** s = "1 + 1"

**Output:** 2 

**Example 2:**

**Input:** s = " 2-1 + 2 "

**Output:** 3 

**Example 3:**

**Input:** s = "(1+(4+5+2)-3)+(6+8)"

**Output:** 23 

**Constraints:**

*   <code>1 <= s.length <= 3 * 10<sup>5</sup></code>
*   `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.
*   `s` represents a valid expression.
*   `'+'` is **not** used as a unary operation (i.e., `"+1"` and `"+(2 + 3)"` is invalid).
*   `'-'` could be used as a unary operation (i.e., `"-1"` and `"-(2 + 3)"` is valid).
*   There will be no two consecutive operators in the input.
*   Every number and running calculation will fit in a signed 32-bit integer.

## Solution

```typescript
function calculate(s: string): number {
    let i = 0

    function helper(ca: string[]): number {
        let num = 0
        let prenum = 0
        let isPlus = true
        while (i < ca.length) {
            const c = ca[i]
            if (c !== ' ') {
                if (c >= '0' && c <= '9') {
                    num = num * 10 + parseInt(c)
                } else if (c === '+') {
                    prenum += num * (isPlus ? 1 : -1)
                    isPlus = true
                    num = 0
                } else if (c === '-') {
                    prenum += num * (isPlus ? 1 : -1)
                    isPlus = false
                    num = 0
                } else if (c === '(') {
                    i++
                    num = helper(ca)
                } else if (c === ')') {
                    prenum += num * (isPlus ? 1 : -1)
                    return prenum
                }
            }
            i++
        }
        return prenum + num * (isPlus ? 1 : -1)
    }
    return helper(s.split(''))
}

export { calculate }
```