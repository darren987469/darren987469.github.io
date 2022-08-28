---
layout: post
title: Algorithm - binary search
subtitle:
tags: binary-search
---

* easy, [852. Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/)
* medium, [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
* hard, [354. Russian Doll Envelopes](https://leetcode.com/problems/russian-doll-envelopes/)

```java
public int peakIndexInMountainArray(int[] arr) {
    int l = 0, r = arr.length - 1;
    while(l < r) {
        int mid = l + (r-l)/2;
        if(arr[mid] < arr[mid+1])
            l = mid + 1;
        else
            r = mid;
    }
    return l;
}
```

* medium, [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

```java
public boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length, n = matrix[0].length;
    int l = 0, r = m*n-1;
    while(l <= r) {
        int mid = l + (r-l)/2;
        int val = matrix[mid / n][mid % n];
        if(val == target)
            return true;
        else if(val > target) {
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }
    return false;
}
```
