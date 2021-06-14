---
layout: post
title: Data structure - Skiplist
subtitle:
tags: skiplist
---

Leetcode:
* hard, [1206. Design Skiplist](https://leetcode.com/problems/design-skiplist/)

A skiplist is a data structure that takes `O(log(n))` time to `add`, `erase`, and `search`.
Application: running medians (moving medians).

```
level4 dummy ---> 30 -------------------------------------------> null
level3 dummy ---> 30 -----------> 50 ---------------------------> null
level2 dummy ---> 30 -----------> 50 -----------> 70------------> null
level1 dummy ---> 30 ---> 40 ---> 50 ---> 60 ---> 70 ---> 90 ---> null
```
Add, erase, search 80 takes `O(log(n))` time.

```java
class Skiplist {
    Node dummy;
    public Skiplist() {
        dummy = new Node(-1, null, null);
    }

    public boolean search(int target) {
        Node node = dummy;
        while(node != null) {
            while(node.next != null && node.next.val < target)
                node = node.next;
            if(node.next != null && node.next.val == target)
                return true;
            node = node.down;
        }
        return false;
    }

    public void add(int num) {
        Stack<Node> prevNodes = new Stack<>();
        Node node = dummy;
        while(node != null) {
            while(node.next != null && node.next.val < num)
                node = node.next;
            prevNodes.push(node);
            node = node.down;
        }
        boolean insert = true;
        Node down = null;
        while(insert && !prevNodes.isEmpty()) {
            node = prevNodes.pop();
            Node newNode = new Node(num, node.next, down);
            node.next = newNode;
            down = newNode;
            insert &= Math.random() <= 0.5;
        }
        if(insert) {
            dummy = new Node(-1, null, dummy);
        }
    }

    public boolean erase(int num) {
        Node node = dummy;
        boolean found = false;
        while(node != null) {
            while(node.next != null && node.next.val < num)
                node = node.next;
            if(node.next != null && node.next.val == num) {
                node.next = node.next.next;
                found = true;
            }
            node = node.down;
        }
        return found;
    }

    class Node {
        int val = -1;
        Node next, down;
        public Node(int val, Node next, Node down) {
            this.val = val;
            this.next = next;
            this.down = down;
        }
    }
}
```

Reference: https://www.youtube.com/watch?v=783qX31AN08
