### Owner
- Stephen

### Question Title
- [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/?tab=Description/)

### Question Description
Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 
[2,3,4] , the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Design a data structure that supports the following two operations:

void addNum(int num) - Add a integer number from the data stream to the data structure.
double findMedian() - Return the median of all elements so far.

For example:
```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

### Question Type
- [x] Heap
- [x] Design

### Follow Up
None

---------------------------------------------------------------------------
# [Solution 1] 


### Thoughts
在Data stream中找到median。這道題是Heap的經典應用，需要同時維護一個最大堆和一個最小堆， 最大堆和最小堆的size <= 當前數字count / 2。在學習heap數據結構的時候一般都會講到這一題，很經典。


### Complexity
- Time: addNum O(logN), findMedian O(1),
- Space: O(n)


### Ref Links
- https://www.cnblogs.com/yrbbest/p/5044819.html

### Source Code
```java
class MedianFinder {
    private PriorityQueue<Integer> maxOrientedHeap;
    private PriorityQueue<Integer> minOrientedHeap;
    
    public MedianFinder() {
        this.minOrientedHeap = new PriorityQueue<Integer>();
        this.maxOrientedHeap = new PriorityQueue<Integer>(10, new Comparator<Integer>() {
                public int compare(Integer i1, Integer i2) {
                    return i2 - i1;
                }
            });
    }
    // Adds a number into the data structure.
    public void addNum(int num) {
        maxOrientedHeap.add(num);               // O(logn)
        minOrientedHeap.add(maxOrientedHeap.poll());               // O(logn)
        if(maxOrientedHeap.size() < minOrientedHeap.size()) {
            maxOrientedHeap.add(minOrientedHeap.poll());        //O(logn)
        }
    }

    // Returns the median of current data stream
    public double findMedian() {                    // O(1)
        if(maxOrientedHeap.size() == minOrientedHeap.size())
            return (maxOrientedHeap.peek() + minOrientedHeap.peek()) / 2.0;
        else
            return maxOrientedHeap.peek();
    }
}; 

```

