**Link** - https://leetcode.com/problems/longest-palindromic-substring/ <br>
**Difficulties** - Medium <br>

**Algo** <br>
For the string `babad`
find
```
ba      -> x
bab     -> found, minimum length -> 3
baba    -> x
babad   -> x
ab      -> skip, cuz minimum found lenght is 3
abad    -> x

answer -> bab
```

**Kotlin Solution**
```
class Solution {
    var longestWord = ""
    fun longestPalindrome(s: String): String {
        for(index in 0..s.length) {
            if(index > s.length - longestWord.length) return longestWord
            for(secondIndex in (index+1+longestWord.length)..s.length) {
                val word = s.substring(index, secondIndex)
                val reverseWord = word.reversed()
                if(word == reverseWord) {
                    if(word.length > longestWord.length) longestWord = word
                }
            }
        }
        return longestWord
    }
}
```

**Note**
To aviod time limit error, take care of return point. We don't need to find every possible pair.