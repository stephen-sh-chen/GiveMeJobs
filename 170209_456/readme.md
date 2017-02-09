### Owner
- George

### Question Title
- [456. 132 Pattern](https://leetcode.com/problems/132-pattern/)

### Question Description
> Given a sequence of n integers a1, a2, ..., an, a 132 pattern is a subsequence ai, aj, ak such that i < j < k and ai < ak < aj. Design an algorithm that takes a list of n numbers as input and checks whether there is a 132 pattern in the list.

Note: n will be less than 15,000.

Example 1:
Input: [1, 2, 3, 4]

Output: False

Explanation: There is no 132 pattern in the sequence.
Example 2:
Input: [3, 1, 4, 2]

Output: True

Explanation: There is a 132 pattern in the sequence: [1, 4, 2].
Example 3:
Input: [-1, 3, 2, 0]

Output: True

Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].
### Question Type
- [x] Stack

### Follow Up
- https://leetcode.com/problems/increasing-triplet-subsequence/

---------------------------------------------------------------------------
# [Solution 1 - Brute Force] 


### Thoughts


### Complexity
- Time:  O(n<sup>3</sup>)
- Space: O(1)


### Ref Links
- https://discuss.leetcode.com/topic/68242/java-solutions-from-o-n-3-to-o-n-for-132-pattern

### Source Code
```java
public boolean find132pattern(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            for (int k = j + 1; k < nums.length; k++) {
                if (nums[i] < nums[k] && nums[k] < nums[j]) return true;
            }
        }
    }
    return false;
}
```

---------------------------------------------------------------------------
---------------------------------------------------------------------------
# [Solution 2 - Stack] 


### Thoughts
下面這種方法利用來棧來做，既簡潔又高效，思路是我們維護一個棧和一個變量third，其中third就是第三個數字，也是pattern 132中的2，棧裡面按順序放所有大於third的數字，也是pattern 132中的3，那麼我們在遍歷的時候，如果當前數字小於third，即pattern 132中的1找到了，我們直接返回true即可，因為已經找到了，注意我們應該從後往前遍歷數組。 如果當前數字大於棧頂元素，那麼我們按順序將棧頂數字取出，賦值給third，然後將該數字壓入棧，這樣保證了棧裡的元素仍然都是大於third的，我們想要的順序依舊存在，進一步來說，棧裡存放的都是可以維持second > third的second值，其中的任何一個值都是大於當前的third值，如果有更大的值進來，那就等於形成了一個更優的second > third的這樣一個組合，並且這時彈出的third值比以前的third值更大，為什麼要保證third值更大，因為這樣才可以更容易的滿足當前的值first比third值小這個條件，參見代碼如下：

### Complexity
- Time:  O(n)
- Space: O(n)


### Ref Links
- https://discuss.leetcode.com/topic/67881/single-pass-c-o-n-space-and-time-solution-8-lines-with-detailed-explanation
- http://www.cnblogs.com/grandyang/p/6081984.html

### Source Code
```java
public class Solution {
    public boolean find132pattern(int[] nums) {
        if(nums == null || nums.length == 0) return false;
        Stack<Integer> stack = new Stack<>();
        int third = Integer.MIN_VALUE;
        
        for(int i = nums.length-1; i>=0;i--){
            if(nums[i] < third) return true;
            else{
                while(!stack.isEmpty() && nums[i] > stack.peek()){
                    third = stack.pop(); 
                }
                stack.push(nums[i]);
            }
        }
        return false;
    }
}
```
