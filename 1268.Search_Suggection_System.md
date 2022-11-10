**Link** - https://leetcode.com/problems/search-suggestions-system/<br>
**Difficulties** - Medium <br>

**Algo**
1. Substring the given searchword to charactor group.
eg. mouse to m, mo, mou, mous, mouse.
2. For each charactor, search in the products array.
3. Only take count when each charactor pair is at the start of the give product.
4. if true, add to the result list

**Kotlin Solution**
```
class Solution {
    fun suggestedProducts(products: Array<String>, searchWord: String): List<List<String>> {
        val sortedArray = products.sorted()
        
        val parentResultList = MutableList(searchWord.length) { mutableListOf<String>() }
        
        for(index in 1..searchWord.length) {
            val eachSearchWord = searchWord.substring(0, index)
            
            var searchResultList = mutableListOf<String>()
            for(product in sortedArray) {
                if(product.indexOf(eachSearchWord) == 0) {
                    searchResultList.add(product)
                }
            }
            if(searchResultList.size > 3) searchResultList = searchResultList.subList(0, 3)
            parentResultList.add(index - 1, searchResultList)
        }
        
        
        return parentResultList.subList(0, searchWord.length)
    }
}
```