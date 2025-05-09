[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 127\. Word Ladder

Hard

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words <code>beginWord -> s<sub>1</sub> -> s<sub>2</sub> -> ... -> s<sub>k</sub></code> such that:

*   Every adjacent pair of words differs by a single letter.
*   Every <code>s<sub>i</sub></code> for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
*   <code>s<sub>k</sub> == endWord</code>

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return _the **number of words** in the **shortest transformation sequence** from_ `beginWord` _to_ `endWord`_, or_ `0` _if no such sequence exists._

**Example 1:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]

**Output:** 5

**Explanation:** One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long. 

**Example 2:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]

**Output:** 0

**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence. 

**Constraints:**

*   `1 <= beginWord.length <= 10`
*   `endWord.length == beginWord.length`
*   `1 <= wordList.length <= 5000`
*   `wordList[i].length == beginWord.length`
*   `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
*   `beginWord != endWord`
*   All the words in `wordList` are **unique**.

## Solution

```typescript
function ladderLength(beginWord: string, endWord: string, wordList: string[]): number {
    const wordSet: Set<string> = new Set(wordList)
    if (!wordSet.has(endWord)) {
        return 0
    }
    let beginSet: Set<string> = new Set([beginWord])
    let endSet: Set<string> = new Set([endWord])
    const visited: Set<string> = new Set()
    let len = 1
    const wordLen = beginWord.length
    while (beginSet.size > 0 && endSet.size > 0) {
        if (beginSet.size > endSet.size) {
            ;[beginSet, endSet] = [endSet, beginSet]
        }
        const tempSet: Set<string> = new Set()
        for (const word of beginSet) {
            const chars = word.split('')
            for (let i = 0; i < wordLen; i++) {
                const oldChar = chars[i]
                for (let c = 97; c <= 122; c++) {
                    chars[i] = String.fromCharCode(c)
                    const nextWord = chars.join('')
                    if (endSet.has(nextWord)) {
                        return len + 1
                    }
                    if (!visited.has(nextWord) && wordSet.has(nextWord)) {
                        tempSet.add(nextWord)
                        visited.add(nextWord)
                    }
                }
                chars[i] = oldChar
            }
        }
        beginSet = tempSet
        len++
    }
    return 0
}

export { ladderLength }
```