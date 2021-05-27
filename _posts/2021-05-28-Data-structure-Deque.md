---
layout: post
title: Data structure - Deque
subtitle:
tags: deque
---

Leetcode:
* hard, [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

```java
// input  { 1,3,-1,-3,5,3,6,7 }, 3
// output { 3,3,-1, 5,5,7 }
public int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    int[] ans = new int[n - k +1];
    Deque<Integer> deque = new ArrayDeque<>();
    for(int i = 0; i < n; i++) {
        if(deque.size() > 0 && i - deque.getFirst() == k)
            deque.removeFirst();
        if(deque.size() > 0 && nums[i] > nums[deque.getLast()])
            deque.removeLast();
        deque.addLast(i);
        if(i - k + 1 >= 0)
            ans[i-k+1] = nums[deque.getFirst()];
    }
    return ans;
}
```
