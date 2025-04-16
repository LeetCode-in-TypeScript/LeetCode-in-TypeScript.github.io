[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 918\. Maximum Sum Circular Subarray

Medium

Given a **circular integer array** `nums` of length `n`, return _the maximum possible sum of a non-empty **subarray** of_ `nums`.

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A **subarray** may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1`, `k2 <= j` with `k1 % n == k2 % n`.

**Example 1:**

**Input:** nums = [1,-2,3,-2]

**Output:** 3

**Explanation:** Subarray [3] has maximum sum 3. 

**Example 2:**

**Input:** nums = [5,-3,5]

**Output:** 10

**Explanation:** Subarray [5,5] has maximum sum 5 + 5 = 10. 

**Example 3:**

**Input:** nums = [-3,-2,-3]

**Output:** -2

**Explanation:** Subarray [-2] has maximum sum -2. 

**Constraints:**

*   `n == nums.length`
*   <code>1 <= n <= 3 * 10<sup>4</sup></code>
*   <code>-3 * 10<sup>4</sup> <= nums[i] <= 3 * 10<sup>4</sup></code>

## Solution

```typescript
function maxSubarraySumCircular(nums: number[]): number {
    let total = 0
    let maxSum = nums[0],
        curMax = 0
    let minSum = nums[0],
        curMin = 0
    for (let num of nums) {
        curMax = Math.max(num, curMax + num)
        maxSum = Math.max(maxSum, curMax)
        curMin = Math.min(num, curMin + num)
        minSum = Math.min(minSum, curMin)
        total += num
    }
    if (maxSum < 0) {
        return maxSum
    }
    return Math.max(maxSum, total - minSum)
}

export { maxSubarraySumCircular }
```