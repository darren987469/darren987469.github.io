---
layout: post
title: Algorithm - Dynamic programming
subtitle:
tags: dynamic-programming
---

Leetcode:
* medium, [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

```java
public boolean canPartition(int[] nums) {
    int sum = 0;
    for(int num : nums) {
        sum += num;
    }
    if(sum % 2 != 0)
        return false;

    int half = sum / 2;
    boolean[] dp = new boolean[half + 1];
    dp[0] = true;
    for(int num: nums) {
        for(int i = half; i >= num; i--) {
            if(dp[i - num] == true)
                dp[i] = true;
        }
    }
    return dp[half];
}
```
* medium, [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)
* hard, [312. Burst Balloons](https://leetcode.com/problems/burst-balloons/submissions/)
