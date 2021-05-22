---
layout: post
title: Data structure - Stack
subtitle:
tags: stack
---

Leetcode:
* hard, [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

```java
public int largestRectangleArea(int[] heights) {
    int n = heights.length;
    int max = 0;
    Stack<Integer> stack = new Stack<>();
    for (int i = 0; i <= n; i++) {
        int height = (i == n) ? 0 : heights[i];
        while (!stack.empty() && height < heights[stack.peek()]) {
            int hh = heights[stack.pop()];
            int width = stack.empty() ? i : i - 1 - stack.peek();
            max = Math.max(max, hh * width);
        }
        stack.push(i);
    }
    return max;
}
```

```java
System.out.println(main.largestRectangleArea(new int[]{0,5,4,1,2})); // 8
System.out.println(main.largestRectangleArea(new int[]{1,2,3,4,5})); // 9
System.out.println(main.largestRectangleArea(new int[]{4,2,0,3,2,5})); // 6
```
