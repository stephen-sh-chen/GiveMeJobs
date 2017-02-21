### Owner
- Luckman

### Question Title
- [60. Permutation Sequence](https://leetcode.com/problems/permutation-sequence/)

### Question Description
> The set [1,2,3,…,n] contains a total of n! unique permutations.
> By listing and labeling all of the permutations in order, We get the following sequence (ie, for n = 3):
```
"123"
"132"
"213"
"231"
"312"
"321"
```
> Given n and k, return the kth permutation sequence.
> Note: Given n will be between 1 and 9 inclusive.



### Question Type
- [x] Math
- [x] Backtracking

### Follow Up


---------------------------------------------------------------------------
# [Solution 1 - ]


### Thoughts
Directly choose the exact direction instead of traverse all possibilities.


### Complexity
- Time: O(n^2)
- Space: O(1)


### Ref Links
-

### Source Code
```java
public String getPermutation(int n, int k){
    // assume n > 0 and k > 0

    //create factoral array
    int[] factor = new int[n];
    factor[0] = 1;
    for(int i = 1; i < n; i++){
        factor[i] = i*factor[i-1];
    }

    StringBuilder sb = new StringBuilder();
    boolean[] check = new boolean[n+1];
    // check n layer
    for(int i = n; i >=1; i--){
        int branch = k/factor[i-1];
        int left = k%factor[i-1];
        // if tree is full
        if(left > 0){
            branch++;
        }
        //update the k
        k -= (branch-1)*factor[i-1];

        // find the (branch)th value of current layer
        int index = 1;
        for(int j = 0; j < branch; j++, index++){
            while(check[index]){
                index++;
            }
        }
        check[--index] = true;
        sb.append(Integer.toString(index));
    }

    return sb.toString();
}
```

