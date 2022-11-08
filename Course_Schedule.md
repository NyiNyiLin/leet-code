**Link** - https://leetcode.com/problems/course-schedule-ii/ <br>
**Difficulties** - Medium <br>

**Algo** <br>
numCourses = 4 <br>
prerequisites = [[1,0],[2,0],[3,1],[3,2]] <br>

1. Create a Hash map based on prerequisites. For example based on above prerequisites. <br>
1 -> 0 <br>
2 -> 0 <br>
3 -> 1, 2 <br>

2. For each subject in harsh list, add prerequisites subject to the result list. <br>
for example, for subject 1, add 0 to the result list, then add 1, <br>
then for subject 2, add 0 to the result list, 0 is already there, skip and only have to add 2. <br>
for 3, need to add 1 to the result list, 1 is already in result list (don't need to check 1 dependency in harsh list), if 1 is not there, check 1 dependcy in harsh list before adding 1 to the result list. <br>
then  2 and etc

**Exit Loop** <br>
For each index in harsh list, create a searchKeyList to keep track of what is currently searching so that we are finding the same loop in the data. <br>
For example, for this prerequisites harsh list <br>
1 -> 5 <br>
2 -> 1 <br>
5 -> 2, 6 <br>


**Kotlin Solution**
```
class Solution {
    val finalCourseList = mutableListOf<Int>()
    val courseHarsh = HashMap<Int, IntArray>()
    var currentSearchKeyList = mutableListOf<Int>()
    var result = 0
        
    fun findOrder(numCourses: Int, prerequisites: Array<IntArray>): IntArray {
        
        if(prerequisites.isEmpty()) {
            for(index in 0..numCourses-1) {
                finalCourseList.add(index)
            }
            return finalCourseList.toIntArray()
        }
        
        
        for(preReq in prerequisites) {
            if(courseHarsh.containsKey(preReq[0])) {
                val courseList = courseHarsh.get(preReq[0])?.toMutableList() ?: mutableListOf<Int>()
                courseList.add(preReq[1])
                courseHarsh.put(
                    preReq[0],
                    courseList.toIntArray()
                )
            } else {
                var courseList = mutableListOf<Int>()
                courseList.add(preReq[1])
                courseHarsh.put(
                    preReq[0],
                    courseList.toIntArray()
                )
            }
        }
        
        courseHarsh.keys.forEach { it ->
            if(result == 0 ) {
                findCourse(it)
                currentSearchKeyList.clear()
            }
        }
        
        if(result == 0 && finalCourseList.size != numCourses) {
            for(index in 0..numCourses-1) {
                if(finalCourseList.contains(index).not()) finalCourseList.add(index)
            }
        }
        
        if(result == -1) finalCourseList.clear() 
        return finalCourseList.toIntArray()
    }

    fun findCourse(key : Int) {
        if(finalCourseList.contains(key)) return
        
        if(courseHarsh.get(key) == null) {
            if(finalCourseList.contains(key).not()) {
                finalCourseList.add(key)
                
            }
            currentSearchKeyList.remove(key)
        }
        
        if(currentSearchKeyList.contains(key)) {
            result = -1
            return
        }
        currentSearchKeyList.add(key)
    
        
        val courseList = courseHarsh.get(key)?.toMutableList() ?: mutableListOf<Int>()
        
        var index = 0
        if(courseList.size != 0) {
            do {
                val key = courseList[index]
                findCourse(key)
                if(result == -1) {
                     index = courseList.size
                } else {
                     index++
                }
             
            } while(index < courseList.size)
        }
        
        
        if(finalCourseList.contains(key).not()) {
            if(result != -1) finalCourseList.add(key)
        }
        currentSearchKeyList.remove(key)
    } 
}
```