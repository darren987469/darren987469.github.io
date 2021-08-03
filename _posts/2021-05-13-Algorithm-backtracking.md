---
layout: post
title: Algorithm - Backtracking
subtitle:
tags: backtracking
---

Leetcode:
* medium, [78. Subsets](https://leetcode.com/problems/subsets/)
* medium, [90. subsets II](https://leetcode.com/problems/subsets-ii/)

### backtrack

```java
List<List<Integer>> ans = new ArrayList<>();
public List<List<Integer>> subsetsWithDup(int[] nums) {
    Arrays.sort(nums);
    backtrack(nums, new ArrayList<>(), 0);
    return ans;
}

public void backtrack(int[] nums, List<Integer> cur, int first) {
    ans.add(new ArrayList<>(cur));
    for(int i = first; i < nums.length; i++) {
        if(i != first && i > 0 && nums[i] == nums[i-1])
            continue;
        cur.add(nums[i]);
        backtrack(nums, cur, i+1);
        cur.remove(cur.size() -1);
    }
}
```

### bitwise

Example: generate subsets of [1,2,3]
binary bitmasks:
000 -> []
001 -> [3]
010 -> [2]
011 -> [2,3]
100 -> [1]
101 -> [1,3]
110 -> [1,2]
111 -> [1,2,3]

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> ans = new ArrayList<>();
    int n = nums.length;
    for(int i = (int)Math.pow(2, n); i < (int)Math.pow(2,n+1); i++) {
        // generate 1000 -> substring(1) -> 000
        String bitmask = Integer.toBinaryString(i).substring(1);

        List<Integer> cur = new ArrayList<>();
        for(int j = 0; j < n; j++) {
            if(bitmask.charAt(j) == '1')
                cur.add(nums[j]);
        }
        ans.add(cur);
    }
    return ans;
}
```
https://leetcode.com/discuss/general-discussion/1073221/All-about-Bitwise-Operations-Beginner-Intermediate

```java
// bitCount
Integer.bitCount(1); // 1
Integer.bitCount(2); // 1
Integer.bitCount(3); // 2

public int bitCount(int n) {
    int count = 0;
    while(n > 0) {
        n = n & (n-1);
        count++;
    }
    return count;
}
```

More:
* hard, [51. N-Queens](https://leetcode.com/problems/n-queens/)
