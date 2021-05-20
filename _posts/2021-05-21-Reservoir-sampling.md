---
layout: post
title: Reservoir sampling
subtitle:
tags: reservoir-sampling
---

Leetcode:
* medium, [382. Linked List Random Node](https://leetcode.com/problems/linked-list-random-node/)

Use reservoir sampling to make sure we sample things randomly without knowing the size.

```java
class Solution {
    ListNode head;
    public Solution(ListNode head) {
        this.head = head;
    }

    /** Returns a random node's value. */
    public int getRandom() {
        int scope = 1, chosenValue = 0;
        ListNode cur = head;
        while(cur != null) {
            if(Math.random() < 1.0 / scope)
                chosenValue = cur.val;
            scope += 1;
            cur = cur.next;
        }
        return chosenValue;
    }
}
```

Proof: the probability is the same with this algorithm

For i-th item, the probability to sample it is `1/i`. When we have (i+1)-th items, the probability to keep i-th item is
`1/i * (1 - 1/(i+1))`. When have n items, it becomes  `1/i * (1 - 1/(i+1)) * (1 - 1/(i+2)) * (1 - 1/n) = 1/n`.

```java
Solution solution = new Solution([1, 2, 3]);
solution.getRandom(); // return 1
solution.getRandom(); // return 3
solution.getRandom(); // return 2
solution.getRandom(); // return 2
solution.getRandom(); // return 3
// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
```
