**Link** - https://leetcode.com/problems/decode-string <br>
**Category** - Recursive <br>
**Difficulties** - Medium <br>

**Algo**
1. Find the Inner "[]" pair
2. Find the number count 4 or 40 or 400
3. loop only one pair "[]" to reconstruct the output string.
4. Repeat till no "[]" is present in the output string.

**Kotlin Soulion**
```
class Solution {
    
    fun findFirstIndex(s: String, startIndex: Int, lastFoundIndex: Int): Int {
        var firstIndex = s.indexOf("[", startIndex)
        val lastIndex = s.indexOf("]")
        if(firstIndex == -1 || lastIndex == -1) return lastFoundIndex 
        val insideIndex = s.indexOf("[", firstIndex+1)
        if(insideIndex != -1 && insideIndex < lastIndex) {
            firstIndex = insideIndex
        }
        return findFirstIndex(s, firstIndex+1, firstIndex)
    }
    
    fun decodeString(s: String): String {
        var result = ""
        var firstIndex = findFirstIndex(s, 0, -1)
        val lastIndex = s.indexOf("]", firstIndex)
    
        // just findd digit 4 or 40 or 400
        if(firstIndex == -1 || lastIndex == -1) return s

        val decodedString = s.substring(firstIndex+1,lastIndex)
    
        var decodeNumber = 0
    
    	if(firstIndex-3 >= 0) {
            val threeDigit = s.substring(firstIndex-3, firstIndex)
            if(threeDigit.toIntOrNull() == null) {
                val twoDigit = s.substring(firstIndex-2, firstIndex)
				if(twoDigit.toIntOrNull() == null) {
                    val oneDigit = s.substring(firstIndex-1, firstIndex)
                    decodeNumber = oneDigit.toInt()
                } else decodeNumber = twoDigit.toInt()
            } else decodeNumber = threeDigit.toInt()
        } else if(firstIndex-2 >= 0) {
            val twoDigit = s.substring(firstIndex-2, firstIndex)
				if(twoDigit.toIntOrNull() == null) {
                    val oneDigit = s.substring(firstIndex-1, firstIndex)
                    decodeNumber = oneDigit.toInt()
                } else decodeNumber = twoDigit.toInt()
        } else {
            val oneDigit = s.substring(firstIndex-1, firstIndex)
            decodeNumber = oneDigit.toInt()
        }
        //
    
        var digitCount = if(decodeNumber > 99) 3 else if(decodeNumber > 9) 2 else 1
        var front = ""
        if(firstIndex-digitCount+1 > 1) {
            front = s.substring(0, firstIndex - digitCount)
        }
        val end = s.substring(lastIndex+1, s.length)
    
        result = front
        for(index in 1..decodeNumber) {
            result = result + decodedString
        }
    
        result = result + end
    
        if(result.contains("[")) {
            result = decodeString(result)
        }

        return result
    }
}
```

**Note**
