**Link** - https://leetcode.com/problems/rotate-image/ <br>
**Difficulties** - Medium <br>

**Algo**

```
1 2 3     1 4 7     7 4 1
4 5 6  => 2 5 8  => 8 5 2
7 8 9     3 6 9     9 6 3
Original  Transpose Reverse
```

**Kotlin Solution**
```
class Solution {
    fun rotate(matrix: Array<IntArray>): Unit {
        var replace = matrix[0][0]
        val total = matrix.size * matrix.size
        
        val reminder = total % 2
        var mid = total / 2
        if(reminder != 0) mid++
        
        var a = matrix.size - 1
        var b = a
        for(x in 0..matrix.size-1) {
            for(y in x..matrix[x].size-1) {
                val temp = matrix[x][y]
                matrix[x][y] = matrix[y][x]
                matrix[y][x] = temp             
            }
        }
        
        for(x in 0..matrix.size-1) {
            for(y in 0..(matrix[x].size/2)-1) {
                val temp = matrix[x][y]
                matrix[x][y] = matrix[x][matrix[x].size-1-y]
                matrix[x][matrix[x].size-1-y] = temp                
            }
        }
    }
}
```

**Disclaimer** <br>
Have to check discussion to solve this problem.