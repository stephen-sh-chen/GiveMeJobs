### Owner
- George

### Question Title
- [525. Contiguous Array](https://leetcode.com/problems/contiguous-array/?tab=Description)

### Question Description
Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.
Examples: 
[0,0,0,1,1,1] , the maximum length is 3 because there are three 0's and three 1's. 

[1,1,1,1], the maximum length is 0 because there is no 0 and four 1's. 


### Question Type
- [x] HashTable

### Follow Up
None

---------------------------------------------------------------------------
# [Solution 1] 


### Thoughts
第一圈先過一變把nums裡面是0的element換成-1, 這樣如果[i,j]之間的sum是零的話, 我們就知道i到j之間零和一出現的次數是一樣的
另外我們必須用HashMap去存每個index目前的sum是多少, 有個要注意的地方是我們要找的條件是When the sum between i and j is 0. 
所以sum要放在HashMap的Key才能做O(1)的搜尋, 如果用map.containsValue(i)解法會變O(n^2)


### Complexity
- Time: O(n), 2n
- Space: O(n)


### Ref Links
- http://massivealgorithms.blogspot.com/2017/02/leetcode-525-contiguous-array.html

### Source Code
```java
public class Solution {
    public int findMaxLength(int[] nums) {
        if(nums.length == 0 || nums == null) {
            return 0;
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) nums[i] = -1;
        }
        
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        int sum = 0, max = 0;
        
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum)) {
                max = Math.max(max, i - map.get(sum));
            }
            else {
                map.put(sum, i);
            }
        }
        
        return max;
    }
}

```

