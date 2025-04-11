[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 201\. Bitwise AND of Numbers Range

Medium

Given two integers `left` and `right` that represent the range `[left, right]`, return _the bitwise AND of all numbers in this range, inclusive_.

**Example 1:**

**Input:** left = 5, right = 7

**Output:** 4 

**Example 2:**

**Input:** left = 0, right = 0

**Output:** 0 

**Example 3:**

**Input:** left = 1, right = 2147483647

**Output:** 0 

**Constraints:**

*   <code>0 <= left <= right <= 2<sup>31</sup> - 1</code>

## Solution

```typescript
function rangeBitwiseAnd(left: number, right: number): number {
    const MASKS: number[] = [
        0x00000000, 0x80000000, 0xc0000000, 0xe0000000, 0xf0000000, 0xf8000000, 0xfc000000, 0xfe000000, 0xff000000,
        0xff800000, 0xffc00000, 0xffe00000, 0xfff00000, 0xfff80000, 0xfffc0000, 0xfffe0000, 0xffff0000, 0xffff8000,
        0xffffc000, 0xffffe000, 0xfffff000, 0xfffff800, 0xfffffc00, 0xfffffe00, 0xffffff00, 0xffffff80, 0xffffffc0,
        0xffffffe0, 0xfffffff0, 0xfffffff8, 0xfffffffc, 0xfffffffe,
    ]
    if (left === right) {
        return left
    }
    const leadingZeros = Math.clz32(left ^ right)
    return right & MASKS[leadingZeros]
}

export { rangeBitwiseAnd }
```