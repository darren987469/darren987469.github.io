---
layout: post
title: Data structure - LinkedList
subtitle:
tags: linkedlist
---

* medium, [2181. Merge Nodes in Between Zeros](https://leetcode.com/problems/merge-nodes-in-between-zeros/)

### Circle detection

* medium, [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

                     <---- f2
                   |        |
                   |        |
s0 ----> s1 ----> s2 ----> s3
fo                f1       f3
<-----------------><-------->
         x             y

slow: moves 1 step at a time
fast: moves 2 steps at a time
x: the length of the linked list before the start of the cycle
y: the distance from the start of the cycle to where `slow` and `fast` met
c: the length of the cycle

slow travels `x + y` steps and fast travels `2 * (x + y)` steps. The extra distance `x + y`
is `n * c`.
Let `slow` starts from y, `fast` starts from the beginning of the list.
After x steps, `slow` and `fast` meets at the start of the cycle.

```java
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while(fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
        if(fast == slow) {
            slow = head;
            while(slow != fast) {
                slow = slow.next;
                fast = fast.next;
            }
            return fast;
        }
    }
    return null;
}
```
