### Owner
- Wayne

### Question Title
- [47. Permutations II](https://leetcode.com/problems/permutations-ii/)

### Question Description
> Given a collection of numbers that might contain duplicates, return all possible unique permutations.
```
For example, given
[1,1,2] have the following unique permutations:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```
### Question Type
- [x] Backtracking

### Follow Up

---------------------------------------------------------------------------
# [Solution 1 - Using Backtracking with HashMap] 


### Thoughts
The basic idea is the duplicated elements should not appear in the same level of recursion.


### Complexity
- Time: 
- Space: 


### Ref Links


### Source Code
```java
public class Solution {
    void backtracking(int[] nums, List<List<Integer>> res, HashMap<Integer, Integer> map, int[] solution, int n) {
        if (n == nums.length) {
            List<Integer> row = new ArrayList<Integer>();
            for (int val : solution) {
                row.add(val);
            }
            res.add(row);
            
            return;
        }
        
        for (Integer key : map.keySet()) {
            int count = map.get(key);
            if (count > 0) {
                map.put(key, count - 1);
                solution[n] = key;
                backtracking(nums, res, map, solution, n + 1);
                map.put(key, map.get(key) + 1);
            }
        }
        
        return;
    }

    public List<List<Integer>> permuteUnique(int[] nums) {    
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        int[] solution = new int[nums.length];
        
        // init hash map to prevent duplicate elements
        for (int i = 0; i < nums.length; i++) {
            Integer num = nums[i];
            if (!map.containsKey(num)) map.put(num, 1);
            else map.put(num, map.get(num) + 1);
        }
        
        backtracking(nums, res, map, solution, 0);
        
        return res;
    }
}
```

---------------------------------------------------------------------------

```