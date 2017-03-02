### Question Title
- [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

### Question Description
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### Question Type
- [x] String
- [x] Backtracking
- [x] DFS

---------------------------------------------------------------------------
# [Solution]


### Thoughts
先把Tree畫出來，觀察何時可以加左括，何時加右括；分析如下：
左括已滿時(等於n)，就可以加右括或把string塞入res List
未滿時，
如果左括==右括，就只能加左括；
但如果左括 > 右括，就左右括都可以加

重點在於這些情況代表全部了嗎？    
左滿 => 右未滿 or 右滿

左未滿 => 右未滿(右不能大於左) => 右==左 or 右<左

### Complexity
- Time:
- Space:


### Ref Links
-

### Source Code
```python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        res = []
        self.helper(n, 0, 0, "", res)
        return res

    def helper(self, n, numLeft, numRight, str, res):
        if numLeft == n:
            if numRight < n:
                self.helper(n, numLeft, numRight+1, str+")", res)
            elif numRight == n:
                res.append(str)
                return
        else:
            if numLeft == numRight:
                self.helper(n, numLeft+1, numRight, str+"(", res)
            elif numLeft > numRight:
                self.helper(n, numLeft+1, numRight, str+"(", res)
                self.helper(n, numLeft, numRight+1, str+")", res)

```

---------------------------------------------------------------------------
# [Solution II]


### Thoughts
簡化上述的判斷式


### Complexity
- Time:
- Space:


### Ref Links
-

### Source Code
```python
def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        res = []
        self.helper(n, 0, 0, "", res)
        return res

    def helper(self, n, numLeft, numRight, str, res):
        if len(str) == n * 2:
            res.append(str)
            return
        if numLeft < n:
            self.helper(n, numLeft+1, numRight, str+"(", res)
        if numRight < numLeft:
            self.helper(n, numLeft, numRight+1, str+")", res)

```
