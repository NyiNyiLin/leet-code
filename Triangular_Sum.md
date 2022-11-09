**Link** - https://leetcode.com/problems/find-triangular-sum-of-an-array/<br>
**Difficulties** - Medium <br>

**Algo**


**Kotlin Solution**
```
class Solution {
    fun triangularSum(nums: IntArray): Int {
       return calculateTriangularSum(nums)
    }
    
    fun calculateTriangularSum(nums: IntArray) : Int {
         val size = nums.size
        if(size == 1) return nums[0]
        val newArray = mutableListOf<Int>()
        for(index in 0..nums.size-2){
            val total = nums[index] + nums[index+1]
            val akwan = total % 10
            newArray.add(akwan)
        }
        return calculateTriangularSum(newArray.toIntArray())
    }
}
```