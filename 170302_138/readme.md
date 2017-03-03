### Owner
- KH

### Question Title
- [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/?tab=Description)

### Question Description
> A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

每個node, 一定會有next,不一定有random

### Question Type
- [x] Hash Table
- [x] Linked List

# [Solution] 

- Solution 1: use hash table

- Solution 2: append same node after the original node the separate into two linkedl list.

### Thoughts


### Complexity

Solution 1

- Time: O(n)
- Space: O(1)

Solution 2

- Time: O(n)
- Space: O(n)

### Source Code
```java
//Solution 1
public RandomListNode copyRandomList(RandomListNode head) {
        RandomListNode node = head;
        while(node != null){
            RandomListNode copy_node = new RandomListNode(node.label);
            copy_node.next = node.next;
            node.next = copy_node;
            node = copy_node.next;
        }
        node = head;
        while(node != null){
            if(node.random != null){ node.next.random = node.random.next; }
            node = node.next.next;
        }
        RandomListNode dummyhead = new RandomListNode(0);
        RandomListNode copy_node =  dummyhead;
        node = head; 
        while(node != null && node.next != null){
            copy_node.next = node.next;
            node.next = node.next.next;
            copy_node = copy_node.next;
            node = node.next;
        }
        return dummyhead.next;
    }

//Solution 2
    public RandomListNode copyRandomList(RandomListNode head) {
      if (head == null) return null;
      
      Map<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
      
      // loop 1. copy all the nodes
      RandomListNode node = head;
      while (node != null) {
        map.put(node, new RandomListNode(node.label));
        node = node.next;
      }
      
      // loop 2. assign next and random pointers
      node = head;
      while (node != null) {
        map.get(node).next = map.get(node.next);
        map.get(node).random = map.get(node.random);
        node = node.next;
      }
      
      return map.get(head);
    }
```
