**Link** - https://leetcode.com/problems/swap-nodes-in-pairs/ <br>
**Category** - Recursive <br>
**Difficulties** - Medium <br>

**Algo**


**Kotlin Solution**
```
/**
 * Example:
 * var li = ListNode(5)
 * var v = li.`val`
 * Definition for singly-linked list.
 * class ListNode(var `val`: Int) {
 *     var next: ListNode? = null
 * }
 */
class Solution {
    fun swapPairs(head: ListNode?): ListNode? {
        if(head== null) return null
                
        var nextNextNode : ListNode? = null
        if(head.next != null) {
            nextNextNode = head?.next
            nextNextNode = nextNextNode.next
        }
        val nextNode = head.next 
        if(head.next != null) {
            nextNode?.next = head
            head.next = swapPairs(nextNextNode) 
            return nextNode
        }
        
        return head
    }
    
}
```
