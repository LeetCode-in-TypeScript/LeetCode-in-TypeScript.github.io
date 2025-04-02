[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 30\. Substring with Concatenation of All Words

Hard

You are given a string `s` and an array of strings `words` of **the same length**. Return all starting indices of substring(s) in `s` that is a concatenation of each word in `words` **exactly once**, **in any order**, and **without any intervening characters**.

You can return the answer in **any order**.

**Example 1:**

**Input:** s = "barfoothefoobarman", words = ["foo","bar"]

**Output:** [0,9]

**Explanation:** Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively. The output order does not matter, returning [9,0] is fine too. 

**Example 2:**

**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]

**Output:** [] 

**Example 3:**

**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]

**Output:** [6,9,12] 

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of lower-case English letters.
*   `1 <= words.length <= 5000`
*   `1 <= words[i].length <= 30`
*   `words[i]` consists of lower-case English letters.

## Solution

```typescript
function findSubstring(s: string, words: string[]): number[] {
    let ans: number[] = []
    let n1 = words[0].length
    let n2 = s.length
    let map1 = new Map<string, number>()

    for (let ch of words) {
        map1.set(ch, (map1.get(ch) ?? 0) + 1)
    }

    for (let i = 0; i < n1; i++) {
        let left = i
        let j = i
        let c = 0
        let map2 = new Map<string, number>()

        while (j + n1 <= n2) {
            let word1 = s.substring(j, j + n1)
            j += n1

            if (map1.has(word1)) {
                map2.set(word1, (map2.get(word1) ?? 0) + 1)
                c++

                while ((map2.get(word1) ?? 0) > (map1.get(word1) ?? 0)) {
                    let word2 = s.substring(left, left + n1)
                    map2.set(word2, (map2.get(word2) ?? 0) - 1)
                    left += n1
                    c--
                }

                if (c === words.length) {
                    ans.push(left)
                }
            } else {
                map2.clear()
                c = 0
                left = j
            }
        }
    }
    return ans
}

export { findSubstring }
```