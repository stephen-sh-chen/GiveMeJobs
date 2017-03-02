### Owner
- Luckman

### Question Title
- [339. Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum/)

### Question Description
> Given a nested list of integers, return the sum of all integers in the list weighted by their depth.
> 
> Each element is either an integer, or a list -- whose elements may also be integers or other lists.
>
> Example 1:
> Given the list [[1,1],2,[1,1]], return 10. (four 1's at depth 2, one 2 at depth 1)
>
> Example 2:
> Given the list [1,[4,[6]]], return 27. (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4*2 + 6*3 = 27)


### Question Type
- [x] DFS BFS

### Follow Up
- (1)Recursion DFS, (2)Iteration DFS, (3)Iteration BFS

---------------------------------------------------------------------------
# [Solution 1 - Recursion DFS] 


### Thoughts
Using Recursion

### Complexity
- Time:  O(V)
- Space: 


### Ref Links


### Source Code
```java
public int depthSum(List<NestedInteger> nestedList) {
    return helper(nestedList, 1);
}

private int helper(List<NestedInteger> nestedList, int layer){
    int total = 0;
    for(NestedInteger i : nestedList){
        if(i.isInteger()){
            total += layer*i.getInteger();
        }else{
            total += helper(i.getList(), layer+1);
        }
    }
    return total;
}
```


---------------------------------------------------------------------------
# [Solution 2 - Iteration DFS] 


### Thoughts
Using Iteration + Stack

### Complexity
- Time:  O(V)
- Space: 


### Ref Links


### Source Code
```java
class Obj{
    List<NestedInteger> list;
    int layer;
    Obj(List<NestedInteger> ls, int num){
        list = ls;
        layer = num;
    }
}

public int depthSum(List<NestedInteger> nestedList) {
    Stack<Obj> stack = new Stack<Obj>();
    stack.push(new Obj(nestedList, 1));
    int sum = 0;
    while(!stack.isEmpty()){
        Obj obj = stack.pop();
        for(NestedInteger i : obj.list){
            if(i.isInteger()){
                sum += i.getInteger() * obj.layer;
            }else{
                stack.push(new Obj(i.getList(), obj.layer+1));
            }
        }
    }
    return sum;
}

```


---------------------------------------------------------------------------
# [Solution 3 - Iteration BFS] 


### Thoughts
Using Iteration + Queue

### Complexity
- Time:  O(V)
- Space: 


### Ref Links


### Source Code
```java
class Obj{
    List<NestedInteger> list;
    int layer;
    Obj(List<NestedInteger> ls, int num){
        list = ls;
        layer = num;
    }
}

public int depthSum(List<NestedInteger> nestedList) {
    Queue<Obj> queue = new LinkedList<Obj>();
    queue.offer(new Obj(nestedList, 1));
    int sum = 0;
    while(!queue.isEmpty()){
        Obj obj = queue.poll();
        for(NestedInteger i : obj.list){
            if(i.isInteger()){
                sum += i.getInteger() * obj.layer;
            }else{
                queue.offer(new Obj(i.getList(), obj.layer+1));
            }
        }
    }
    return sum;
}
```
