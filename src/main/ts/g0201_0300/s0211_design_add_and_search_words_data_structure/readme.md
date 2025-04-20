[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 211\. Design Add and Search Words Data Structure

Medium

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

*   `WordDictionary()` Initializes the object.
*   `void addWord(word)` Adds `word` to the data structure, it can be matched later.
*   `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

**Example:**

**Input**

    ["WordDictionary","addWord","addWord","addWord","search","search","search","search"] [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
    
**Output**

    [null,null,null,null,false,true,true,true]

**Explanation**

    WordDictionary wordDictionary = new WordDictionary();
    wordDictionary.addWord("bad");
    wordDictionary.addWord("dad");
    wordDictionary.addWord("mad");
    wordDictionary.search("pad"); // return False
    wordDictionary.search("bad"); // return True
    wordDictionary.search(".ad"); // return True
    wordDictionary.search("b.."); // return True 

**Constraints:**

*   `1 <= word.length <= 500`
*   `word` in `addWord` consists lower-case English letters.
*   `word` in `search` consist of `'.'` or lower-case English letters.
*   At most `50000` calls will be made to `addWord` and `search`.

## Solution

```typescript
interface TrieNode {
    [key: string]: TrieNode | boolean
}

class WordDictionary {
    root: TrieNode

    constructor() {
        this.root = {}
    }

    addWord(word: string): void {
        let current = this.root
        for (let i = 0; i < word.length; i++) {
            const letter = word[i]
            if (!current.hasOwnProperty(letter)) {
                current[letter] = {}
            }
            current = current[letter] as TrieNode
        }
        current.end = true
    }

    search(word: string): boolean {
        const searchSubtree = (word: string, index: number, subtree: TrieNode) => {
            if (word.length === index) {
                return subtree.hasOwnProperty('end')
            }
            const currentLetter = word[index]
            index += 1
            if (currentLetter === '.') {
                return Object.keys(subtree).some((letter) => searchSubtree(word, index, subtree[letter] as TrieNode))
            } else {
                if (subtree.hasOwnProperty(currentLetter)) {
                    return searchSubtree(word, index, subtree[currentLetter] as TrieNode)
                } else {
                    return false
                }
            }
        }
        return searchSubtree(word, 0, this.root)
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * var obj = new WordDictionary()
 * obj.addWord(word)
 * var param_2 = obj.search(word)
 */

export { WordDictionary }
```