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
* medium, [583. Delete Operation for Two Strings](https://leetcode.com/problems/delete-operation-for-two-strings/)
* medium, [740. Delete and Earn](https://leetcode.com/problems/delete-and-earn/)
* medium, [799. Champagne Tower](https://leetcode.com/problems/champagne-tower/)
* medium, [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
* hard, [1092. Shortest Common Supersequence](https://leetcode.com/problems/shortest-common-supersequence/)

Longest common subsequence video, https://www.youtube.com/watch?v=ASoaQq66foQ
