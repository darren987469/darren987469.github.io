---
layout: post
title: Data structure - HashMap
subtitle:
tags: HashMap
---

Leetcode:
* easy, [706. Design HashMap](https://leetcode.com/problems/design-hashmap/)


Collision: Use linked list to handle collision.

A HashMap with 4 capacity.

       LinkedList head     value (key, val)
[0]
[1] -> {-1,-1} ----------> {1,1}
[2] -> {-1,-1} ----------> {2,3} -------> {6,5} // collision
[3]

```java
Map<Integer, Integer> map = new MyHashMap<>();
map.put(1,1);
map.put(2,3);
map.put(6,5);
```

```java
class MyHashMap {

    /** Initialize your data structure here. */
    ListNode[] nodes;
    public MyHashMap() {
        nodes = new ListNode[10000];
    }

    /** value will always be non-negative. */
    public void put(int key, int value) {
        int index = getIndex(key);
        if(nodes[index] == null)
            nodes[index] = new ListNode(-1, -1);
        ListNode prev = find(nodes[index], key);
        if(prev.next == null)
            prev.next = new ListNode(key, value);
        else
            prev.next.val = value;
    }

    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    public int get(int key) {
        int index = getIndex(key);
        if(nodes[index] == null)
            return -1;
        ListNode prev = find(nodes[index], key);
        return prev.next == null ? -1 : prev.next.val;
    }

    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    public void remove(int key) {
        int index = getIndex(key);
        if(nodes[index] == null)
            return;
        ListNode prev = find(nodes[index], key);
        if(prev.next == null)
            return;
        prev.next = prev.next.next;
    }

    private ListNode find(ListNode bucket, int key) {
        ListNode node = bucket, prev = null;
        while(node != null && node.key != key) {
            prev = node;
            node = node.next;
        }
        return prev;
    }

    private int getIndex(int key) {
        return key % nodes.length;
    }

    class ListNode {
        int key, val;
        ListNode next;
        public ListNode(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
}
```

* easy, [525. Contiguous Array](https://leetcode.com/problems/contiguous-array/)
* medium, [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
