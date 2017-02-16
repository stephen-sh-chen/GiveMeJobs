### Owner
- Leo

### Question Title
- [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

### Question Description
> Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.
The same repeated number may be chosen from C unlimited number of times.
Note:
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set [2, 3, 6, 7] and target 7,
A solution set is:

```
[
  [7],
  [2, 2, 3]
]
```

### Question Type
- [x] Array
- [x] Backtracking

### Follow Up
Each number in C may only be used once in the combination.

---------------------------------------------------------------------------
# [Solution - Combination Sum]


### Thoughts
DFS + [剪枝](http://imgur.com/a/hSowh)

### Complexity
- Time:
- Space:


### Ref Links
-

### Source Code
```python
class Solution(object):
    def combinationSum(self, candidates, target):
        res = []
        self.helper(candidates, target, 0, [], res)
        return res

    def helper(self, candidates, target, index, curList, res):
        if target < 0:
            pass
        elif 0 == target:
            res.append(curList)
        elif 0 < target:
            for i in xrange(index, len(candidates)):
                self.helper(candidates, target-candidates[i], i, curList+[candidates[i]], res)
```

---------------------------------------------------------------------------
# [Solution - Combination Sum II ]


### Thoughts
DFS + [剪枝](http://imgur.com/a/hSowh),
從下一個開始(i + 1)

### Complexity
- Time:
- Space:


### Ref Links
-

### Source Code
```python
class Solution(object):
    def combinationSum2(self, candidates, target):
        res = []
        candidates.sort()
        self.helper(candidates, target, 0, [], res)        
        return res

    def helper(self, nums, target, index, curList, res):
        if target < 0:
            return
        elif target == 0:
            res.append(curList)
            return
        else:
            for i in xrange(index, len(nums)):
                if i > index and nums[i-1] == nums[i]:
                    continue
                self.helper(nums, target-nums[i], i+1, curList+[nums[i]], res)

```
