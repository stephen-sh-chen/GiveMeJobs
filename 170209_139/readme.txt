### Owner
- Stephen

### Question Title
- [139. Word Break](https://leetcode.com/problems/word-break/)

### Question Description
> Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.
```
For example, given
s = "leetcode",
dict = ["leet", "code"].
```
> Return true because "leetcode" can be segmented as "leet code".
UPDATE (2017/1/4):
The wordDict parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.

### Question Type
- [x] Dynamic Programming
- [x] BFS

### Follow Up
Can you output all the possible valid brokend words

---------------------------------------------------------------------------
# [Solution 1 - Using DP] 


### Thoughts
This problem can be solved using dp algorithm, use a array to check if there is a valid break or not for all substrings ending in the array's index.

### Complexity
- Time: O(n<sup>2</sup>)
- Space: O(n)


### Ref Links
- https://roy3221.gitbooks.io/algorithms/content/CH5%20DP/leetcode_139_word_break.html

### Source Code
```java
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict) {
        boolean[] validBreakAtIndex = new boolean[s.length()+1];
        validBreakAtIndex[0] = true; 
        // use a nested loop that will check all substrings of s. 
        for(int i = 1; i < s.length()+1; i++) {
            for(int j = 0; j < i; j++) {
           //  validBreakAtIndex[j] = false, which means there is no valid break at index j, so in this case, we do not need to check substring of (j,i).  
 // validbreakAtIndex[j] = true, which means there is a valid break at index j, so in this case, we just need to check if substring(j,i) is a valid word, because if(j,j+1) is a valid word, then validBreakAtIndex[j+1] = true, which will be checked when j+1. 
                if(validBreakAtIndex[j] && wordDict.contains(s.substring(j,i))) {
                    validBreakAtIndex[i] = true;
                    break;
                }
            }
        }
        return validBreakAtIndex[s.length()];
    }
}
```

---------------------------------------------------------------------------
# [Solution 2 - Using BFS] 


### Thoughts
cited from https://leetcode.com/discuss/8479/a-solution-using-bfs

People have posted elegant solutions using DP. The solution I post below using BFS is no better than those. Just to share some new thoughts. We can use a graph to represent the possible solutions. The vertices of the graph are simply the positions of the first characters of the words and each edge actually represents a word. For example, the input string is "nightmare", there are two ways to break it, "night mare" and "nightmare".

The graph would be
0-->5-->9


The question is simply to check if there is a path from 0 to 9. The most efficient way is traversing the graph using BFS with the help of a queue and a hash set. The hash set is used to keep track of the visited nodes to avoid repeating the same work.
For this problem, the time complexity is O(n^2) and space complexity is O(n), the same with DP. This idea can be used to solve the problem word break II. We can simple construct the graph using BFS, save it into a map and then find all the paths using DFS.

### Complexity
- Time: O(n<sup>2</sup>)
- Space: O(n)


### Ref Links
- https://roy3221.gitbooks.io/algorithms/content/CH5%20DP/leetcode_139_word_break.html

### Source Code
```java
public boolean wordBreak(String s, Set<String> dict) {
    if (dict.contains(s)) return true;
    Queue<Integer> queue = new LinkedList<Integer>();
    queue.offer(0);
    // use a set to record checked index to avoid repeated work.
    // This is the key to reduce the running time to O(N^2).
    Set<Integer> visited = new HashSet<Integer>();
    visited.add(0);
    while (!queue.isEmpty()) {
        int curIdx = queue.poll();
        for (int i = curIdx+1; i <= s.length(); i++) {
            if (visited.contains(i)) continue;
            if (dict.contains(s.substring(curIdx, i))) {
                if (i == s.length()) return true;
                queue.offer(i);
                visited.add(i);
            }
        }
    }
    return false;
}
```