[![](https://img.shields.io/github/stars/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript)
[![](https://img.shields.io/github/forks/LeetCode-in-TypeScript/LeetCode-in-TypeScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-TypeScript/LeetCode-in-TypeScript/fork)

## 68\. Text Justification

Hard

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified and no extra space is inserted between words.

**Note:**

*   A word is defined as a character sequence consisting of non-space characters only.
*   Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
*   The input array `words` contains at least one word.

**Example 1:**

**Input:** words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16

**Output:** [ "This is an", "example of text", "justification. " ]

**Example 2:**

**Input:** words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16

**Output:** [ "What must be", "acknowledgment ", "shall be " ]

**Explanation:** Note that the last line is "shall be " instead of "shall be", because the last line must be left-justified instead of fully-justified. Note that the second line is also left-justified becase it contains only one word.

**Example 3:**

**Input:** words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20

**Output:** [ "Science is what we", "understand well", "enough to explain to", "a computer. Art is", "everything else we", "do " ]

**Constraints:**

*   `1 <= words.length <= 300`
*   `1 <= words[i].length <= 20`
*   `words[i]` consists of only English letters and symbols.
*   `1 <= maxWidth <= 100`
*   `words[i].length <= maxWidth`

## Solution

```typescript
function fullJustify(words: string[], maxWidth: number): string[] {
    const output: string[] = []
    let sb: string[] = []
    let lineTotal = 0
    let numWordsOnLine = 0
    let startWord = 0
    for (let i = 0; i < words.length - 1; i++) {
        lineTotal += words[i].length
        numWordsOnLine++
        if (lineTotal + numWordsOnLine + words[i + 1].length > maxWidth) {
            sb = []
            if (numWordsOnLine === 1) {
                sb.push(words[i])
                while (lineTotal++ < maxWidth) {
                    sb.push(' ')
                }
            } else {
                const spaces = Math.floor((maxWidth - lineTotal) / (numWordsOnLine - 1))
                let extraSp = (maxWidth - lineTotal) % (numWordsOnLine - 1)

                for (let j = startWord; j < startWord + numWordsOnLine - 1; j++) {
                    sb.push(words[j])
                    sb.push(' '.repeat(spaces + (extraSp-- > 0 ? 1 : 0)))
                }
                sb.push(words[startWord + numWordsOnLine - 1])
            }
            output.push(sb.join(''))
            startWord = i + 1
            numWordsOnLine = lineTotal = 0
        }
    }

    // Handle last line
    sb = []
    lineTotal = 0
    for (let i = startWord; i < words.length; i++) {
        lineTotal += words[i].length
        sb.push(words[i])
        if (lineTotal < maxWidth) {
            sb.push(' ')
            lineTotal++
        }
    }
    while (lineTotal < maxWidth) {
        sb.push(' ')
        lineTotal++
    }
    output.push(sb.join(''))

    return output
}

export { fullJustify }
```