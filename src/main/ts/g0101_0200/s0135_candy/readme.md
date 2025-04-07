[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 135\. Candy

Hard

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

*   Each child must have at least one candy.
*   Children with a higher rating get more candies than their neighbors.

Return _the minimum number of candies you need to have to distribute the candies to the children_.

**Example 1:**

**Input:** ratings = [1,0,2]

**Output:** 5

**Explanation:** You can allocate to the first, second and third child with 2, 1, 2 candies respectively. 

**Example 2:**

**Input:** ratings = [1,2,2]

**Output:** 4

**Explanation:** You can allocate to the first, second and third child with 1, 2, 1 candies respectively. The third child gets 1 candy because it satisfies the above two conditions. 

**Constraints:**

*   `n == ratings.length`
*   <code>1 <= n <= 2 * 10<sup>4</sup></code>
*   <code>0 <= ratings[i] <= 2 * 10<sup>4</sup></code>

## Solution

```typescript
function candy(ratings: number[]): number {
    const n = ratings.length
    const candies: number[] = new Array(n).fill(1)
    for (let i = 0; i < n - 1; i++) {
        if (ratings[i + 1] > ratings[i]) {
            candies[i + 1] = candies[i] + 1
        }
    }
    for (let i = n - 1; i > 0; i--) {
        if (ratings[i - 1] > ratings[i] && candies[i - 1] < candies[i] + 1) {
            candies[i - 1] = candies[i] + 1
        }
    }
    return candies.reduce((sum, c) => sum + c, 0)
}

export { candy }
```