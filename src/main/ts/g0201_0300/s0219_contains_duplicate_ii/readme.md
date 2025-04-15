[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 219\. Contains Duplicate II

Easy

Given an integer array `nums` and an integer `k`, return `true` if there are two **distinct indices** `i` and `j` in the array such that `nums[i] == nums[j]` and `abs(i - j) <= k`.

**Example 1:**

**Input:** nums = [1,2,3,1], k = 3

**Output:** true 

**Example 2:**

**Input:** nums = [1,0,1,1], k = 1

**Output:** true 

**Example 3:**

**Input:** nums = [1,2,3,1,2,3], k = 2

**Output:** false 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   <code>0 <= k <= 10<sup>5</sup></code>

## Solution

```typescript
function containsNearbyDuplicate(nums: number[], k: number): boolean {
    const s = new Set()
    for (let i = 0, l = nums.length; i < l; i++) {
        if (i > k) {
            s.delete(nums[i - k - 1])
        }
        if (s.has(nums[i])) {
            return true
        }
        s.add(nums[i])
    }
    return false
}

export { containsNearbyDuplicate }
```