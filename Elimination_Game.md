**Link** - https://leetcode.com/problems/elimination-game/ <br>
**Difficulties** - Medium <br>

**Algo** <br>
 to update and record head in each turn. when the total number becomes 1, head is the only number left.

When will head be updated? <br>

1. if we move from left 
2. if we move from right and the total remaining number % 2 == 1

like 2 4 6 8 10, we move from 10, we will take out 10, 6 and 2, head is deleted and move to 4

like 2 4 6 8 10 12, we move from 12, we will take out 12, 8, 4, head is still remaining 2

then we find a rule to update our head.

`(head = head + step)`

**Kotlin Solution** <br>
```
class Solution {
    fun lastRemaining(n: Int): Int {        
        
        var left = true
        var remaining = n
        var step = 1
        var head = 1
        
        while(remaining > 1) {
            if(left || remaining % 2 == 1) {
                head = head + step
            }
            remaining = remaining / 2;
            step = step * 2;
            left = left.not()
        }
        return head
    }
}
```

**Disclaimer** <br>
Have to check discussion to solve this problem.

-----------


**Recursive Solution** <br>
(Face Time limit error when n = 10 power 8)

**Algo** <br>
Start with the second line. Cuz second line always start with 2, 4, etc
The loop is according to the problem description.
Remove seocond number in each loop.

**Kotlin Solution**
```
class Solution {
    fun lastRemaining(n: Int): Int {        
        if(n == 1) return n
        var list = mutableListOf<Int>()
        for(index in 1..n/2) {
            list.add(index*2)
        }
        
        return remove2(list, false)
    }

    fun remove2(list: MutableList<Int>, isFront: Boolean) : Int {
        if(list.size == 1) return list[0]
        
        if(isFront) {
            val newList = mutableListOf<Int>()
            for(index in 0..list.size/2) {
                if((index*2)+1 < list.size) newList.add(list[(index*2)+1])
            }
            return remove2(newList, isFront.not())
        } else {
            var newNewList = mutableListOf<Int>()
            var size = list.size % 2
            for(index in list.size/2 downTo 0) {
                if((index*2)+size < list.size) newNewList.add(list[(index*2)+size])
            }
            newNewList.reverse()
            return remove2(newNewList, isFront.not())
        }
    }

}
```