---
layout: post
title: Data structure - Tree
subtitle:
tags: segment-tree
---

### Segment Tree

Leetcode:
* medium, [307. Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/)

Get sum of then range: time complexity `O(log(n))`.
Update value in the range: time complexity `O(log(n))`.
Space complexity: `O(2n) = O(n)`.

```java
class NumArray {
    int[] tree;
    int n;
    public NumArray(int[] nums) {
        if(nums.length > 0) {
            n = nums.length;
            tree = new int[n * 2];
            buildTree(nums);
        }
    }

    public void update(int index, int val) {
        index += n;
        tree[index] = val;
        while(index > 0) {
            int left = index;
            int right = index;
            if(index % 2 == 0)
                right = index + 1;
            else
                left = index - 1;
            tree[index / 2] = tree[left] + tree[right];
            index /= 2;
        }
    }

    public int sumRange(int left, int right) {
        left += n;
        right += n;
        int sum = 0;
        while(l <= r) {
            if((l % 2) == 1) {
                sum += tree[l]
                l++;
            }
            if((r % 2 == 0)) {
                sum += tree[r];
                r--;
            }
            l /= 2;
            r /= 2;
        }
        return sum;
    }

    private void buildTree(int[] nums) {
        for(int i = n, j = 0; i < 2 * n; i++, j++)
            tree[i] = nums[j];
        for(int i = n -1; i > 0; i--)
            tree[i] = tree[i * 2] + tree[i * 2 + 1];
    }
}
```

Full binary tree
full binary tree can be defined as a binary tree in which all the nodes have two children except the leaf nodes.

Complete binary tree
A binary tree is said to be a complete binary tree when all the levels are completely filled except the last level, which is filled from the left.
