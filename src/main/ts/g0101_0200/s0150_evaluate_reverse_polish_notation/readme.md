[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 150\. Evaluate Reverse Polish Notation

Medium

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

**Example 1:**

**Input:** tokens = ["2","1","+","3","\*"]

**Output:** 9

**Explanation:** ((2 + 1) \* 3) = 9 

**Example 2:**

**Input:** tokens = ["4","13","5","/","+"]

**Output:** 6

**Explanation:** (4 + (13 / 5)) = 6 

**Example 3:**

**Input:** tokens = ["10","6","9","3","+","-11","\*","/","\*","17","+","5","+"]

**Output:** 22

**Explanation:**

    ((10 \* (6 / ((9 + 3) \* -11))) + 17) + 5
    = ((10 \* (6 / (12 \* -11))) + 17) + 5
    = ((10 \* (6 / -132)) + 17) + 5
    = ((10 \* 0) + 17) + 5
    = (0 + 17) + 5
    = 17 + 5
    = 22 

**Constraints:**

*   <code>1 <= tokens.length <= 10<sup>4</sup></code>
*   `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

## Solution

```typescript
function evalRPN(tokens: string[]): number {
    const numberStack: number[] = []
    const isOperator = (val: string): boolean => val === '+' || val === '-' || val === '*' || val === '/'
    for (let token of tokens) {
        if (isOperator(token)) {
            const right = numberStack.pop() as number
            const left = numberStack.pop() as number

            if (token === '+') numberStack.push(left + right)
            else if (token === '-') numberStack.push(left - right)
            else if (token === '*') numberStack.push(left * right)
            else if (token === '/') {
                const result = left / right
                numberStack.push(result < 0 ? Math.ceil(result) : Math.floor(result))
            }
        } else numberStack.push(+token)
    }
    return numberStack.pop() || 0
}

export { evalRPN }
```