[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 433\. Minimum Genetic Mutation

Medium

A gene string can be represented by an 8-character long string, with choices from `'A'`, `'C'`, `'G'`, and `'T'`.

Suppose we need to investigate a mutation from a gene string `start` to a gene string `end` where one mutation is defined as one single character changed in the gene string.

*   For example, `"AACCGGTT" --> "AACCGGTA"` is one mutation.

There is also a gene bank `bank` that records all the valid gene mutations. A gene must be in `bank` to make it a valid gene string.

Given the two gene strings `start` and `end` and the gene bank `bank`, return _the minimum number of mutations needed to mutate from_ `start` _to_ `end`. If there is no such a mutation, return `-1`.

Note that the starting point is assumed to be valid, so it might not be included in the bank.

**Example 1:**

**Input:** start = "AACCGGTT", end = "AACCGGTA", bank = ["AACCGGTA"]

**Output:** 1 

**Example 2:**

**Input:** start = "AACCGGTT", end = "AAACGGTA", bank = ["AACCGGTA","AACCGCTA","AAACGGTA"]

**Output:** 2 

**Example 3:**

**Input:** start = "AAAAACCC", end = "AACCCCCC", bank = ["AAAACCCC","AAACCCCC","AACCCCCC"]

**Output:** 3 

**Constraints:**

*   `start.length == 8`
*   `end.length == 8`
*   `0 <= bank.length <= 10`
*   `bank[i].length == 8`
*   `start`, `end`, and `bank[i]` consist of only the characters `['A', 'C', 'G', 'T']`.

## Solution

```typescript
function minMutation(startGene: string, endGene: string, bank: string[]): number {
    const isInBank = (set: Set<string>, cur: string): string[] => {
        const res: string[] = []
        for (const each of set) {
            let diff = 0
            for (let i = 0; i < each.length; i++) {
                if (each[i] !== cur[i]) {
                    diff++
                    if (diff > 1) break
                }
            }
            if (diff === 1) {
                res.push(each)
            }
        }
        return res
    }
    const set = new Set(bank)
    const queue: string[] = [startGene]
    let step = 0
    while (queue.length > 0) {
        const curSize = queue.length
        for (let i = 0; i < curSize; i++) {
            const cur = queue.shift()!
            if (cur === endGene) {
                return step
            }
            for (const next of isInBank(set, cur)) {
                queue.push(next)
                set.delete(next)
            }
        }
        step++
    }
    return -1
}

export { minMutation }
```